### @props-basic:
<details>
<summary>@props 子コンポーネントで親からのデータを受け取る（基本）</summary>

**Vue.js**  
```vue
<!-- ParentComponent.vue -->
<template>
  <ChildComponent title="こんにちは" :count="5" />
</template>

<script setup>
import ChildComponent from './ChildComponent.vue'
</script>
```

```vue
<!-- ChildComponent.vue -->
<template>
  <div>
    title: {{ title }}<br />
    count: {{ count }}<br />
  </div>
</template>

<script setup>
import { defineProps } from 'vue'

const props = defineProps({
  title: String,
  count: Number
})
</script>
```
</details>

---

### @props-default:
<details>
<summary>@props 型とデフォルト値・必須チェックを付ける</summary>

**Vue.js**  
```vue
<template>
  <div>
    ユーザー名: {{ username }}<br />
    年齢: {{ age }}<br />
  </div>
</template>

<script setup>
import { defineProps, withDefaults } from 'vue'

const props = withDefaults(defineProps<{
  username: string
  age?: number
}>(), {
  age: 18
})
</script>
```
</details>

---

### @props-object:
<details>
<summary>@props 複雑なオブジェクト型を渡す</summary>

**Vue.js**  
```vue
<!-- ParentComponent.vue -->
<template>
  <UserCard :user="userData" />
</template>

<script setup>
import UserCard from './UserCard.vue'

const userData = {
  id: 1,
  name: '山田太郎',
  email: 'taro@example.com'
}
</script>
```

```vue
<!-- UserCard.vue -->
<template>
  <div>
    <h3>{{ user.name }}</h3>
    <p>{{ user.email }}</p>
  </div>
</template>

<script setup>
const props = defineProps({
  user: {
    type: Object,
    required: true
  }
})
</script>
```
</details>

---

### @props-callback:
<details>
<summary>@props 関数を受け取ってコールバックを使う</summary>

**Vue.js**  
```vue
<!-- ParentComponent.vue -->
<template>
  <ChildComponent :onClick="handleClick" />
</template>

<script setup>
import ChildComponent from './ChildComponent.vue'

function handleClick() {
  alert('親コンポーネントの関数が呼ばれました')
}
</script>
```

```vue
<!-- ChildComponent.vue -->
<template>
  <button @click="onClick">クリック</button>
</template>

<script setup>
const props = defineProps({
  onClick: {
    type: Function,
    required: true
  }
})
</script>
```
</details>

---

### @props-filter:
<details>
<summary>@props フィルタ・ソート・検索向けに配列と関数を渡す</summary>

**Vue.js**  
```vue
<!-- ParentComponent.vue -->
<template>
  <ItemList :items="products" :filterFn="isInStock" />
</template>

<script setup>
import ItemList from './ItemList.vue'

const products = [
  { name: 'りんご', stock: 10 },
  { name: 'バナナ', stock: 0 },
  { name: 'みかん', stock: 5 }
]

function isInStock(item) {
  return item.stock > 0
}
</script>
```

```vue
<!-- ItemList.vue -->
<template>
  <ul>
    <li v-for="item in filteredItems" :key="item.name">
      {{ item.name }} (在庫: {{ item.stock }})
    </li>
  </ul>
</template>

<script setup>
import { computed } from 'vue'

const props = defineProps({
  items: Array,
  filterFn: Function
})

const filteredItems = computed(() => props.items.filter(props.filterFn))
</script>
```
</details>
