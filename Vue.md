@props-basic:
<details> 
  <summary>子コンポーネントで親からのデータを受け取る</summary>
vue
コピーする
編集する
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
親から文字列 title と数値 count を受け取ります。

</details>
