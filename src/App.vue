<template>
  <div>
    我是Vue子应用
    <button @click="onSendParent">发送全局消息</button>
    <div v-if="state.content">
      <div style="color: red">{{ state.content }}</div>
    </div>
  </div>
</template>
<script lang="ts" setup>
import { reactive, onMounted } from "vue";
import type { EventCenterForMicroApp } from "@micro-zoe/micro-app";
const state = reactive<{ content: string }>({
  content: "",
});

const onSendParent = () => {
  const ma: EventCenterForMicroApp = (window as any)?.microApp;
  ma.forceSetGlobalData({
    content: "我是Vue子应用发送的全局消息！！！！",
  });
};

onMounted(() => {
  const ma: EventCenterForMicroApp = (window as any)?.microApp;
  ma.addGlobalDataListener((data: { content: string }) => {
    console.log("全局数据", data);
    state.content = data.content;
  });
});
</script>
<style lang="less" scoped></style>