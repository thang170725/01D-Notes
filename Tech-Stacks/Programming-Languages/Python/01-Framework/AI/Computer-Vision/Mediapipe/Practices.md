- [Hand Tracking (nhận diện 21 điểm trên bàn tay)](#hand-tracking-nhận-diện-21-điểm-trên-bàn-tay)
- [Đếm số theo ngón tay](#đếm-số-theo-ngón-tay)
---
# Hand Tracking (nhận diện 21 điểm trên bàn tay)
```python
import cv2
import mediapipe as mp

mp_hands = mp.solutions.hands
mp_draw = mp.solutions.drawing_utils

cap = cv2.VideoCapture(0)

with mp_hands.Hands() as hands:
    while True:
        ret, frame = cap.read()

        rgb = cv2.cvtColor(frame, cv2.COLOR_BGR2RGB)
        result = hands.process(rgb)

        if result.multi_hand_landmarks:
            for hand in result.multi_hand_landmarks:
                mp_draw.draw_landmarks(frame, hand, mp_hands.HAND_CONNECTIONS)

        cv2.imshow("Hand", frame)

        if cv2.waitKey(1) == 27:
            break
```
# Đếm số theo ngón tay
```bash
1. bật camera
2. nhận diện bàn tay
3. khi bạn giơ 1 ngón → hiện số 1
4. giơ 2 ngón → hiện số 2
```