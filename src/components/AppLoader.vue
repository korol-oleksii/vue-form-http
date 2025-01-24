<template>
  <div class="loading"></div>
</template>

<style scoped>
.loading {
  width: 24px;
  height: 24px;
  flex: 0 0 auto;
  border-radius: 50%;
  background: conic-gradient(#0000 10%, #FF9100);
  mask: radial-gradient(farthest-side, #0000 calc(100% - 4px), #000 0);
  animation: aLoading 2s infinite linear;
  margin: 24px auto;
}
@keyframes aLoading {
  0% {
    transform: rotate(-360deg);
  }
  100% {
    transform: rotate(360deg);
  }
}
</style>
