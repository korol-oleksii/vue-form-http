<template>
  <Transition name="fade">
    <div class="hint-auto-close" v-if="autoHintForce" :class="autoHintForce.type">
      <div class="hint-desc">
        <p>{{ autoHintForce.text }}</p>
      </div>
    </div>
  </Transition>
</template>

<script>
export default {
  props: ['autoHintForce']
}
</script>

<style lang="scss" scoped>
  .hint-auto-close {
    background-color: rgba(64, 64, 64, 1);
    box-shadow: 0 8px 16px 0 rgba(0, 0, 0, 0.2);
    border-radius: 8px;
    transform: translate(-50%, -50%);
    padding: 8px;
    position: absolute;
    top: 50%;
    left: 50%;
    width: 224px;

    &.primary {
      background-color: #2c3e50;

      p {
        color: #fff;
      }
    }

    .hint-desc {
      text-align: center;
    }

    p {
      font-size: 14px;
      line-height: 18px;
      color: #fff;
      padding: 0;
    }
  }
</style>
