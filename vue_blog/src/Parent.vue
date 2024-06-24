<script setup lang="ts">
import Child from './components/Child.vue'
import { ref } from 'vue';

// 親→子の関数を発火（ref）
// 子→親の関数を発火（emit）

// 親コンポーネント
// ボタン：子の入力値によってアクティブ・非アクティブ

// 子コンポーネント
// フォーム：親のボタンが押下されたら子のイベント発火（文字数を表示）

// emit・refの使うシーンを明確にする
// 文字数を表示するアプリケーション

const isDisabled = ref<boolean>(true)
  const child = ref<InstanceType<typeof Child> | null>(null)
// const child = ref()

const activeButton = (val: bool) => {
  isDisabled.value = val
}

const clickButton = () => {
  child.value.calcLen()
}

</script>

<template>
  <div>
    <Child 
      ref="child"
      @change-button="activeButton" 
    />
    <button :disabled=isDisabled @click="clickButton">Click</button>
  </div>
</template>

<style scoped>

</style>
