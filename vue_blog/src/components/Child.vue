<script setup lang="ts">
import {ref} from "vue"
// 親→子の関数を発火（ref）
// 子→親の関数を発火（emit）

// 親コンポーネント
// ボタン：子の入力値によってアクティブ・非アクティブ

// 子コンポーネント
// フォーム：親のボタンが押下されたら子のイベント発火（文字数を表示）

// emit・refの使うシーンを明確にする
// 文字数を表示するアプリケーション

const message = ref<string>("")
const len = ref<string>("")

const emits = defineEmits<{(e: 'change-button', val: bool): void}>()
const testEmit = () => {
  if (message.value) {
    emits('change-button', false)
  }else{
    emits('change-button', true)
  }
}

const calcLen = () => {
  len.value = message.value.length + "文字です。"
}

defineExpose({calcLen,});
</script>

<template>
  <div>
    <p>Message is: {{ message }}</p>
    <input v-model="message" @input="testEmit">
    <p v-if="len">{{ len }}</p>
  </div>
</template>