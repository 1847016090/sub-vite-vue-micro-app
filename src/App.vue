<template>
  <div>我是Vue子应用{{state.count}}</div>
</template>
<script lang="ts" setup>
import { reactive } from 'vue'
const state = reactive({
    count: 1
})
</script>
<style lang="less" scoped></style>