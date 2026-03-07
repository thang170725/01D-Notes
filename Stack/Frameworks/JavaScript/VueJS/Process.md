async / await
async function loadData() {
  try {
    const data = await fetchData()
    console.log(data)
  } catch (e) {
    console.error(e)
  }
}


👉 Dễ đọc hơn .then()
# computed – Giá trị tính toán
```bash
- Tạo giá trị phụ thuộc vào dữ liệu khác.
- Tự cập nhật khi dữ liệu gốc đổi.
```
```js
<script setup>
import { ref, computed } from 'vue'

const price = ref(100)
const quantity = ref(2)

const total = computed(() => {
  return price.value * quantity.value
})
</script>

<template>
  <p>Total: {{ total }}</p>
</template>

- Tự động cập nhật
- Tối ưu performance hơn function thường
```

# get() & set()
```js
const fullName = computed({
  get() {
    return firstName.value + ' ' + lastName.value
  },
  set(val) {
    const parts = val.split(' ')
    firstName.value = parts[0]
    lastName.value = parts[1]
  },
})
```

```bash
- Vue chỉ cho dữ liệu chảy theo 1 chiều
    + CHA  ──(props)──▶  CON
    + CHA  ◀─(emit)───  CON
- Con KHÔNG được sửa trực tiếp dữ liệu của Cha
- Con chỉ được:
    + NHẬN dữ liệu → defineProps
    + BÁO lại Cha → defineEmits
    + Nếu bạn nắm được sơ đồ này → 90% Vue sẽ sáng ra.
```
defineProps()
Luồng dữ liệu cha -> Con
**Ex**
```js
<script setup>
import { ref } from 'vue'
import Child from './Child.vue'

const title = ref('Xin chào')
</script>

<template>
  <Child :title="title" />
</template>

- Cha có dữ liệu: title
```
**Component CON**
```js
<script setup>
const props = defineProps({
  title: String
})
</script>

<template>
  <h1>{{ props.title }}</h1>
</template>
```

# defineEmits()
```bash
- Luồng dữ liệ con -> cha.
- VẤN ĐỀ
    + Con không được sửa props, vậy làm sao báo Cha sửa?
    + CÂU TRẢ LỜI: emit event
```
**Ex**
**Component con**
```js
<script setup>
const emit = defineEmits(['changeTitle'])

function clickMe() {
  emit('changeTitle', 'Tiêu đề mới')
}
</script>

<template>
  <button @click="clickMe">Đổi tiêu đề</button>
</template>
```
**Component cha**
```js
<script setup>
import { ref } from 'vue'
import Child from './Child.vue'

const title = ref('Xin chào')

function onChangeTitle(newTitle) {
  title.value = newTitle
}
</script>

<template>
  <h1>{{ title }}</h1>
  <Child @changeTitle="onChangeTitle" />
</template>
```
ifecycle hooks – vòng đời component
<script setup>
import { onMounted, onUnmounted } from 'vue'

onMounted(() => {
  console.log('Component mounted')
})

onUnmounted(() => {
  console.log('Component destroyed')
})
</script>
# ref()
```bash
- Tạo biến reactive có thể thay đổi và Vue tự cập nhật giao diện.
```
```js
<script setup>
import { ref } from 'vue'

const count = ref(0)

const increase = () => {
  count.value++
}
</script>

<template>
  <p>Count: {{ count }}</p>
  <button @click="increase">+</button>
</template>

- Lưu ý:
  + Trong <script>: phải dùng .value
  + Trong <template>: KHÔNG cần .value
```
**Ex: ref với object**
```js
const user = ref({
  name: '',
  age: 0,
})

user.value.name = 'An'
user.value.age = 20
```

# reactive – Object reactive
Dùng khi có object nhiều field
```vue
<script setup>
import { reactive } from 'vue'

const user = reactive({
  name: 'Thắng',
  age: 22
})

const growUp = () => {
  user.age++
}
</script>

<template>
  <p>{{ user.name }} - {{ user.age }}</p>
  <button @click="growUp">Tăng tuổi</button>
</template>


📌 Khác ref:

Không cần .value

Chỉ dùng cho object / array
```
# Directive : (v-bind) – Binding dữ liệu
```bash
- : là viết tắt của v-bind
- Dùng để nối dữ liệu JS với HTML
- :abc="xyz" -> abc nhận GIÁ TRỊ của biến xyz
```
**Trường hợp không dùng binding**
```bash
<template>
  <img src="avatar.png">
</template>

- src cố định, JS không can thiệp được.
```
**Ex**
```js
<img :src="avatar">

- Nghĩa là: Lấy giá trị biến avatar trong JS → gán cho thuộc tính src
```
**Ex**
```js
<template>
  <img :src="avatar" width="150">
</template>

<script setup>
import { ref } from 'vue'

const avatar = ref('https://vuejs.org/logo.png')
</script>

- Kết quả:
    + Vue đọc avatar
    + Gán vào src
    + Khi avatar đổi → ảnh đổi
```

## Demo thay đổi giá trị → UI đổi (quan trọng)
```js
<script setup>
  import { ref } from 'vue'

  const color = ref('red')
  const changeColor = () => {
    color.value = 'blue'
  }
</script>

<template>
  <p :style="{ color: color }">
    Dòng chữ này đổi màu
  </p>

  <button @click="changeColor">Đổi màu</button>
</template>
```

VẬY abc LÀ GÌ? CÓ TỰ ĐẶT KHÔNG?

👉 PHỤ THUỘC abc LÀ GÌ

🔹 TRƯỜNG HỢP 1: PROP BẠN TỰ ĐỊNH NGHĨA → ✔️ TỰ ĐẶT
Component con
defineProps({
  title: String
})

Component cha
<Child :title="title" />


👉 title là:

do bạn đặt

con và cha phải trùng tên

✔️ TÙY Ý đặt tên

🔹 TRƯỜNG HỢP 2: v-model → ❌ KHÔNG ĐƯỢC TỰ ĐẶT
<Child v-model="title" />


Vue bắt buộc dùng:

:modelValue="title"
@update:modelValue="..."


👉 Các tên này là quy ước của Vue

modelValue

update:modelValue

❌ Không đổi thành myValue, value123

🔹 TRƯỜNG HỢP 3: COMPONENT THƯ VIỆN (Dialog, Input…) → ❌ KHÔNG TỰ ĐẶT
<Dialog v-model="show" />


👉 Dialog đã định nghĩa sẵn:

prop nào

event nào

Bạn phải dùng đúng tên nó yêu cầu

3️⃣ SAU DẤU = LÀ GÌ?
:abc="xyz"


👉 xyz:

là biến JS

là expression

do bạn tự đặt

✔️ Hoàn toàn tự do

4️⃣ VÍ DỤ ĐỐI CHIẾU DỄ NHỚ
Ví dụ A – Tự đặt
<Child :hello="msg" />

defineProps({ hello: String })


✔️ OK

Ví dụ B – Sai vì không trùng tên
<Child :hi="msg" />

defineProps({ hello: String })


❌ Con nhận undefined

5️⃣ VÍ DỤ VỚI v-model (NHỚ KỸ)
Vue viết ngầm
<Child v-model="title" />


⇓

<Child
  :modelValue="title"
  @update:modelValue="title = $event"
/>


👉 modelValue KHÔNG PHẢI do bạn đặt

**Nếu đổi giá trị avatar để image thay đổi thì tại sao không đổi trong src đi mà lại đổi trong biến avatar làm gì, một cái là đổi một lần trong src, một cái là đổi thông qua biến rồi gán lại vào src**
v-for – Lặp danh sách
<script setup>
const items = ['Vue', 'React', 'Angular']
</script>

<template>
  <ul>
    <li v-for="(item, index) in items" :key="index">
      {{ item }}
    </li>
  </ul>
</template>
# v-html 
```bash
- Dùng để render (hiển thị) chuỗi HTML như HTML thật, thay vì hiển thị nó như text bình thường.
- v-html = “nhét HTML động vào DOM”
```
**Ex: Không dùng v-html**
```js
<template>
  <p>{{ content }}</p>
</template>

<script setup>
const content = '<b>Xin chào</b>'
</script>

- Kết quả hiển thị trên màn hình: <b>Xin chào</b>
- HTML không được render, chỉ là chữ.
```
**Ex: Dùng v-html**
```js
<template>
  <p v-html="content"></p>
</template>

<script setup>
const content = '<b>Xin chào</b>'
</script>

- Kết quả hiển thị: Xin chào. Thẻ <b> được hiểu là HTML thật.
```
# v-if / v-show – Điều kiện hiển thị
```bash
<p v-if="isLogin">Đã đăng nhập</p>
<p v-else>Chưa đăng nhập</p>
<p v-show="isLogin">Ẩn/hiện bằng CSS</p>

- Khác nhau:
    + v-if: render / destroy
    + v-show: chỉ toggle display
```
# v-model – Two-way binding
```bash
- binding 2 chiều (two-way binding)
v-model THẬT RA LÀ GÌ?

Dòng này 👇

<Child v-model="title" />


Vue sẽ tự dịch ngầm thành 👇

<Child
  :modelValue="title"
  @update:modelValue="title = $event"
/>
```

```js
<script setup>
import { ref } from 'vue'

const name = ref('')
</script>

<template>
  <input v-model="name">
  <p>Xin chào {{ name }}</p>
</template>

Rất hay dùng trong form
```
# @ là viết tắt của v-on

<button @click="handleClick">Click me</button>

<script setup>
const handleClick = () => {
  alert('Hello Vue')
}
</script>

Câu hỏi này rất đúng chỗ cần hiểu 👍
Mình trả lời thẳng – rõ – không vòng vo:

@edit, @reload trong ví dụ này là DO COMPONENT CON TỰ ĐỊNH NGHĨA,
KHÔNG phải Vue có sẵn.

Giờ mình giải thích theo đúng thứ bạn NHÌN THẤY.

1️⃣ @ LÀ GÌ?
@edit="openEdit"


👉 @ chỉ là viết tắt của:

v-on:edit="openEdit"


👉 Nghĩa là:

“Khi có sự kiện tên là edit → chạy hàm openEdit”

2️⃣ edit, reload CÓ SẴN KHÔNG?

❌ KHÔNG CÓ SẴN TRONG VUE

Vue CHỈ có sẵn các event HTML như:

@click

@input

@change

Còn:

@edit
@reload


👉 là event TỰ TẠO

3️⃣ AI TẠO RA @edit, @reload?

👉 Component CON (SimpleItemListView) tạo ra

Bên trong SimpleItemListView.vue sẽ có dạng:

const emit = defineEmits(['edit', 'reload'])

4️⃣ LUỒNG NHÌN THẤY RÕ RÀNG
Component CHA
<SimpleItemListView
  :rows="rows"
  :columns="columns"
  @edit="openEdit"
  @reload="items.reload()"
/>


👉 CHA nói:

Nếu CON báo edit → chạy openEdit

Nếu CON báo reload → gọi items.reload()

Component CON (bên trong)
emit('edit', row)
emit('reload')


👉 Khi CON chạy mấy dòng này:

CHA sẽ chạy code tương ứng

5️⃣ VÍ DỤ CỤ THỂ (NHÌN RÕ)
CON
emit('edit', item)

CHA
@edit="openEdit"


👉 Vue tự làm:

openEdit(item)

6️⃣ KHI NÀO EVENT LÀ CÓ SẴN?
HTML
<button @click="save" />


👉 click là event của HTML → CÓ SẴN

Component Vue
<MyComp @click="save" />


👉 click chỉ tồn tại nếu:

MyComp emit('click')

hoặc Vue forward event

7️⃣ BẢNG NHỚ NHANH
Dạng	Ai định nghĩa
@click (button)	HTML
@input (input)	HTML
@edit (component)	COMPONENT CON
@reload	COMPONENT CON
@update:modelValue	VUE (quy ước)
8️⃣ CÂU KẾT LUẬN (RẤT QUAN TRỌNG)

Bất kỳ @ten-gi-do nào trên component
đều PHẢI được component đó emit ra.

Nếu bạn muốn, bước tiếp theo mình có thể:

🧪 Viết SimpleItemListView giả lập để bạn thấy emit('edit')

🚫 Chỉ ra lỗi hay gặp: dùng @edit nhưng quên emit

🧠 Giải thích vì sao @click trên component đôi khi không chạy

🔁 Áp lại vào code thật của bạn

👉 Bạn muốn tiếp phần nào?

# watch()
```bash
- Theo dõi sự thay đổi
- Dùng khi muốn làm gì đó khi data thay đổi
- Hay dùng cho:
  + Gọi API
  + Validate
  + Lưu localStorage
```
```vue
<script setup>
import { ref, watch } from 'vue'

const age = ref(18)

watch(age, (newAge, oldAge) => {
  console.log('old:', oldAge)
  console.log('new:', newAge)
})
</script>

<template>
  <input type="number" v-model="age">
</template>
```
**Ex**
```js
watch(
  () => props.item,
  (val) => {
    console.log('item changed', val)
  }
)
```
immediate: true là gì?
watch(
  source,
  callback,
  { immediate: true }
)


👉 Callback chạy ngay lần đầu, không đợi thay đổi

# watchEffect – Watch tự động
Vue tự phát hiện dependency
```bash
watchEffect(() => {
  // code
})
```

```bash
<script setup>
import { ref, watchEffect } from 'vue'

const age = ref(18)

watchEffect(() => {
  console.log('Age hiện tại:', age.value)
})
</script>

<template>
  <input type="number" v-model="age">
</template>

Console:
Age hiện tại: 18   // chạy NGAY
Age hiện tại: 20   // khi bạn gõ
Age hiện tại: 21


📌 Điểm khác với watch:

watchEffect chạy lần đầu

watch thì không (mặc định)
```