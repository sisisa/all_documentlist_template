## @defineprops(@props)

### props-basic:
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
### props-object:
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

### props-callback:
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

### props-filter:
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

## @defineEmit(@emit)

### defineEmit-basic:
<details>
<summary>@defineEmit 子コンポーネントから親へイベントを発火する（基本）</summary>

**Vue.js - Composition API**

子コンポーネントから親コンポーネントにイベントを通知したい場合、Vue.jsのComposition APIでは `defineEmits()` を使用します。

以下は、ボタンをクリックしたときに `"clicked"` というイベントを親へ通知する最小構成の例です。

```vue
<!-- ChildComponent.vue -->
<template>
  <button @click="handleClick">クリック</button>
</template>

<script setup>
// イベント名を定義
const emit = defineEmits(['clicked'])

// イベント発火関数
const handleClick = () => {
  emit('clicked')
}
</script>

<!-- ParentComponent.vue -->
<template>
  <!-- 子コンポーネントから "clicked" イベントを受け取る -->
  <ChildComponent @clicked="onChildClicked" />
</template>

<script setup>
import ChildComponent from './ChildComponent.vue'

// イベントハンドラ
const onChildClicked = () => {
  console.log('子コンポーネントでクリックされました')
}
</script>
