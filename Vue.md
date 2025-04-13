
---

## Vue.js の Props 使い方まとめ

以下は、Vue.js の `props` に関するよく使うパターンとその説明です。

<details>
<summary>@props: 基本的な使い方</summary>

```javascript
export default {
  props: {
    title: {
      type: String,
      required: true,
    },
  },
}
