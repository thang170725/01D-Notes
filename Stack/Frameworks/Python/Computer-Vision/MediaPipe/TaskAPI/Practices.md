- [Detect các điểm trên bàn tay](#detect-các-điểm-trên-bàn-tay)
- [Chơi trò chơi dinosaurs bằng MediaPipe + OpenCV](#chơi-trò-chơi-dinosaurs-bằng-mediapipe--opencv)
- [Chơi trò chơi xe leo núi bằng MediaPipe + OpenCV](#chơi-trò-chơi-xe-leo-núi-bằng-mediapipe--opencv)
---
# Detect các điểm trên bàn tay
```python
import cv2
import mediapipe as mp

from mediapipe.tasks import python
from mediapipe.tasks.python import vision


# 1 load model
base_options = python.BaseOptions(
    model_asset_path="hand_landmarker.task"
)

# 2 cấu hình task
options = vision.HandLandmarkerOptions(
    base_options=base_options,
    running_mode=vision.RunningMode.IMAGE
)

# 3 tạo detector
detector = vision.HandLandmarker.create_from_options(options)


# 4 mở camera
cap = cv2.VideoCapture(0)

while True:

    ret, frame = cap.read()
    if not ret:
        break

    rgb = cv2.cvtColor(frame, cv2.COLOR_BGR2RGB)

    # 5 convert sang mp.Image
    mp_image = mp.Image(
        image_format=mp.ImageFormat.SRGB,
        data=rgb
    )

    # 6 chạy model
    result = detector.detect(mp_image)

    # 7 đọc landmarks
    if result.hand_landmarks:

        for landmark in result.hand_landmarks[0]:

            h, w, _ = frame.shape

            x = int(landmark.x * w)
            y = int(landmark.y * h)

            cv2.circle(frame, (x, y), 5, (0,255,0), -1)

    cv2.imshow("hand", frame)

    if cv2.waitKey(1) == 27:
        break

cap.release()
```
# Chơi trò chơi dinosaurs bằng MediaPipe + OpenCV
```python
import cv2
import mediapipe as mp
import math
import pyautogui
import time

from mediapipe.tasks import python
from mediapipe.tasks.python import vision


# -----------------------------
# MODEL
# -----------------------------
base_options = python.BaseOptions(
    model_asset_path="hand_landmarker.task"
)

options = vision.HandLandmarkerOptions(
    base_options=base_options,
    running_mode=vision.RunningMode.VIDEO,
    num_hands=1
)

detector = vision.HandLandmarker.create_from_options(options)


# -----------------------------
# SETTINGS
# -----------------------------
OPEN_THRESHOLD = 220   # độ mở tay
cooldown = 0.25       # chống spam space


last_jump = 0


# -----------------------------
# CAMERA
# -----------------------------
cap = cv2.VideoCapture(0)

cap.set(cv2.CAP_PROP_FRAME_WIDTH,640)
cap.set(cv2.CAP_PROP_FRAME_HEIGHT,480)


start_time = time.time()


while True:

    ret, frame = cap.read()

    if not ret:
        continue

    frame = cv2.flip(frame,1)

    h,w,_ = frame.shape


    rgb = cv2.cvtColor(frame,cv2.COLOR_BGR2RGB)

    mp_image = mp.Image(
        image_format=mp.ImageFormat.SRGB,
        data=rgb
    )

    timestamp = int((time.time()-start_time)*1000)

    result = detector.detect_for_video(mp_image,timestamp)


    if len(result.hand_landmarks) > 0:

        hand = result.hand_landmarks[0]

        # palm center
        palm = hand[9]

        px = int(palm.x*w)
        py = int(palm.y*h)

        cv2.circle(frame,(px,py),8,(255,0,255),-1)


        # fingertip indexes
        tips = [4,8,12,16,20]

        total_distance = 0


        for t in tips:

            tip = hand[t]

            tx = int(tip.x*w)
            ty = int(tip.y*h)

            cv2.circle(frame,(tx,ty),8,(0,255,0),-1)

            cv2.line(frame,(px,py),(tx,ty),(255,255,0),2)

            dist = math.sqrt((tx-px)**2 + (ty-py)**2)

            total_distance += dist


        # -----------------------------
        # HAND STATE
        # -----------------------------
        if total_distance > OPEN_THRESHOLD:

            state = "OPEN"

            now = time.time()

            if now - last_jump > cooldown:

                pyautogui.press("space")
                last_jump = now

        else:

            state = "CLOSED"


        # -----------------------------
        # DEBUG
        # -----------------------------
        cv2.putText(frame,f"Hand:{state}",
                    (30,40),
                    cv2.FONT_HERSHEY_SIMPLEX,
                    1,(0,255,0),2)

        cv2.putText(frame,f"Distance:{int(total_distance)}",
                    (30,80),
                    cv2.FONT_HERSHEY_SIMPLEX,
                    0.8,(0,255,255),2)


    cv2.imshow("Dino Hand Control",frame)

    if cv2.waitKey(1)==27:
        break


cap.release()
cv2.destroyAllWindows()
```
# Chơi trò chơi xe leo núi bằng MediaPipe + OpenCV
```python
import cv2
import mediapipe as mp
import math
import pyautogui
import time
import threading

from mediapipe.tasks import python
from mediapipe.tasks.python import vision


# -----------------------------
# MODEL
# -----------------------------
base_options = python.BaseOptions(
    model_asset_path="hand_landmarker.task"
)

options = vision.HandLandmarkerOptions(
    base_options=base_options,
    running_mode=vision.RunningMode.VIDEO,
    num_hands=2
)

detector = vision.HandLandmarker.create_from_options(options)


# -----------------------------
# SETTINGS
# -----------------------------
STEER_THRESHOLD = 25
TOP_ZONE = 0.4
BOTTOM_ZONE = 0.6
OPEN_HAND_DISTANCE = 300


# -----------------------------
# GLOBAL FRAME
# -----------------------------
latest_frame = None
frame_lock = threading.Lock()

running = True


# -----------------------------
# CAMERA THREAD
# -----------------------------
def camera_loop():

    global latest_frame, running

    cap = cv2.VideoCapture(0)

    cap.set(cv2.CAP_PROP_FRAME_WIDTH,640)
    cap.set(cv2.CAP_PROP_FRAME_HEIGHT,480)

    while running:

        ret, frame = cap.read()

        if not ret:
            continue

        frame = cv2.flip(frame,1)

        with frame_lock:
            latest_frame = frame.copy()

    cap.release()


# -----------------------------
# VISION THREAD
# -----------------------------
def vision_loop():

    global latest_frame, running

    start_time = time.time()

    current_lr = "STRAIGHT"
    current_ud = "NONE"

    while running:

        with frame_lock:

            if latest_frame is None:
                continue

            frame = latest_frame.copy()

        h,w,_ = frame.shape

        rgb = cv2.cvtColor(frame,cv2.COLOR_BGR2RGB)

        mp_image = mp.Image(
            image_format=mp.ImageFormat.SRGB,
            data=rgb
        )

        timestamp = int((time.time()-start_time)*1000)

        result = detector.detect_for_video(mp_image,timestamp)


        # -----------------------------
        # DRAW ZONES
        # -----------------------------
        top_line = int(h*TOP_ZONE)
        bottom_line = int(h*BOTTOM_ZONE)

        cv2.line(frame,(0,top_line),(w,top_line),(0,255,255),2)
        cv2.line(frame,(0,bottom_line),(w,bottom_line),(0,255,255),2)

        cv2.putText(frame,"UP",(10,top_line-10),
                    cv2.FONT_HERSHEY_SIMPLEX,0.6,(0,255,255),2)

        cv2.putText(frame,"DOWN",(10,bottom_line+30),
                    cv2.FONT_HERSHEY_SIMPLEX,0.6,(0,255,255),2)


        if len(result.hand_landmarks)==2:

            hand1 = result.hand_landmarks[0][9]
            hand2 = result.hand_landmarks[1][9]

            x1 = int(hand1.x*w)
            y1 = int(hand1.y*h)

            x2 = int(hand2.x*w)
            y2 = int(hand2.y*h)


            # draw hands
            cv2.circle(frame,(x1,y1),10,(0,0,255),-1)
            cv2.circle(frame,(x2,y2),10,(0,0,255),-1)

            cv2.line(frame,(x1,y1),(x2,y2),(0,255,0),3)


            # midpoint
            cx = int((x1+x2)/2)
            cy = int((y1+y2)/2)

            cv2.circle(frame,(cx,cy),8,(255,0,255),-1)

            # horizontal reference
            cv2.line(frame,(0,cy),(w,cy),(255,0,0),2)


            # -----------------------------
            # FIND LEFT HAND
            # -----------------------------
            if x1 < x2:
                lx,ly = x1,y1
            else:
                lx,ly = x2,y2

            cv2.circle(frame,(lx,ly),12,(255,255,0),-1)


            # -----------------------------
            # STEERING
            # -----------------------------
            dy = ly - cy

            if dy < -STEER_THRESHOLD:
                lr = "RIGHT"

            elif dy > STEER_THRESHOLD:
                lr = "LEFT"

            else:
                lr = "STRAIGHT"


            if lr != current_lr:

                pyautogui.keyUp("left")
                pyautogui.keyUp("right")

                if lr == "LEFT":
                    pyautogui.keyDown("left")

                elif lr == "RIGHT":
                    pyautogui.keyDown("right")

                current_lr = lr


            # -----------------------------
            # UP DOWN
            # -----------------------------
            avg_y = (y1+y2)/2

            if avg_y < top_line:
                ud = "UP"

            elif avg_y > bottom_line:
                ud = "DOWN"

            else:
                ud = "NONE"


            if ud != current_ud:

                pyautogui.keyUp("up")
                pyautogui.keyUp("down")

                if ud == "UP":
                    pyautogui.keyDown("up")

                elif ud == "DOWN":
                    pyautogui.keyDown("down")

                current_ud = ud


            # -----------------------------
            # SPACE (hands open)
            # -----------------------------
            distance = math.sqrt((x2-x1)**2 + (y2-y1)**2)

            if distance > OPEN_HAND_DISTANCE:
                pyautogui.press("space")


            # -----------------------------
            # DEBUG
            # -----------------------------
            cv2.putText(frame,f"dy:{int(dy)}",
                        (30,40),
                        cv2.FONT_HERSHEY_SIMPLEX,
                        0.8,(0,255,255),2)

            cv2.putText(frame,f"LR:{lr}",
                        (30,80),
                        cv2.FONT_HERSHEY_SIMPLEX,
                        1,(0,255,0),2)

            cv2.putText(frame,f"UD:{ud}",
                        (30,120),
                        cv2.FONT_HERSHEY_SIMPLEX,
                        1,(0,255,0),2)

            cv2.putText(frame,f"Dist:{int(distance)}",
                        (30,160),
                        cv2.FONT_HERSHEY_SIMPLEX,
                        0.8,(255,255,0),2)


        cv2.imshow("Steering Debug",frame)

        if cv2.waitKey(1)==27:
            running = False
            break


# -----------------------------
# START THREADS
# -----------------------------
t1 = threading.Thread(target=camera_loop)
t2 = threading.Thread(target=vision_loop)

t1.start()
t2.start()

t1.join()
t2.join()

cv2.destroyAllWindows()
```