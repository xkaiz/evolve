<template>
  <router-view />
</template>
<script>
// 解决ERROR ResizeObserver loop completed with undelivered notifications.问题
const debounce = (fn, delay) => {
  let timer = null;
  return function () {
    let context = this;
    let args = arguments;
    clearTimeout(timer);
    timer = setTimeout(function () {
      fn.apply(context, args);
    }, delay);
  }
}
// 解决ERROR ResizeObserver loop completed with undelivered notifications.问题
const _ResizeObserver = window.ResizeObserver;
window.ResizeObserver = class ResizeObserver extends _ResizeObserver {
  constructor(callback) {
    callback = debounce(callback, 16);
    super(callback);
  }
}
</script>
<style>
#app {
  text-align: center;
}
</style>
