- [div key=""](#div-key)
---
# div key=""
```bash
key là một thuộc tính đặc biệt (special prop) giúp React nhận diện duy nhất mỗi phần tử trong một danh sách để tối ưu việc render và cập nhật UI.

Ví dụ:

<div key={1}>Bench Press</div>
<div key={2}>Squat</div>
<div key={3}>Deadlift</div>

Ở đây:

key={1} → React biết đây là phần tử số 1.
key={2} → React biết đây là phần tử số 2.
key={3} → React biết đây là phần tử số 3.
Tại sao cần key?

Giả sử bạn render danh sách:

const exercises = [
  { id: 1, name: "Bench" },
  { id: 2, name: "Squat" },
  { id: 3, name: "Deadlift" },
];

return (
  <>
    {exercises.map((item) => (
      <div key={item.id}>
        {item.name}
      </div>
    ))}
  </>
);

Lần đầu React thấy:

1 Bench
2 Squat
3 Deadlift

Sau đó dữ liệu đổi thành:

1 Bench
3 Deadlift

React nhìn vào key:

key=1  -> vẫn còn
key=2  -> bị xóa
key=3  -> vẫn còn

Nó chỉ xóa phần tử có key=2, thay vì render lại toàn bộ danh sách.

Nếu không có key

React sẽ cảnh báo:

Warning: Each child in a list should have a unique "key" prop.

Vì React không biết phần tử nào là phần tử cũ, phần tử nào là phần tử mới.

Tại sao không nên dùng index?

Nhiều người viết:

{exercises.map((item, index) => (
    <div key={index}>
        {item.name}
    </div>
))}

Nếu sau này chèn thêm phần tử đầu danh sách:

Bench
Squat
Deadlift

thành

Push Up
Bench
Squat
Deadlift

thì tất cả index đều thay đổi:

0 Push Up
1 Bench
2 Squat
3 Deadlift

React tưởng rằng tất cả phần tử đều thay đổi, có thể gây:

render không cần thiết,
mất state của component con,
lỗi với input, animation,...

Vì vậy chỉ dùng index khi danh sách cố định, không thêm/xóa/sắp xếp lại.

Nên dùng gì làm key?

Ưu tiên dùng ID duy nhất từ database:

<div key={exercise.exercise_id}>

Hoặc với dữ liệu của bạn:

{exercises.map((exercise) => (
    <ExerciseCard
        key={exercise.workout_plan_item_id}
        exercise={exercise}
    />
))}

workout_plan_item_id là một lựa chọn rất tốt vì nó là khóa chính và duy nhất.

Còn <div key=></div> thì sao?

Nếu bạn viết:

<div key=""></div>

hoặc

<div key={undefined}></div>

thì gần như không có ý nghĩa. Nếu nhiều phần tử có cùng key rỗng hoặc undefined, React sẽ coi chúng là trùng key và có thể cảnh báo hoặc cập nhật UI không chính xác.

Tóm lại
key chỉ có ý nghĩa khi render danh sách (map()).
key phải duy nhất trong danh sách đó.
Nên dùng ID từ database (workout_plan_item_id, exercise_id, ...).
Không nên dùng index nếu danh sách có thể thay đổi thứ tự hoặc thêm/xóa phần tử.
Với một <div> đơn lẻ không nằm trong danh sách, key thường không cần thiết và React sẽ bỏ qua
```