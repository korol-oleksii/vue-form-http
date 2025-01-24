<template>
  <div class="content__row" v-for="item in resumeData.contentBlocks" :key="item.type">
    <div class="resume-subtitle">
      <div v-if="item.type === 'subtitle'">
        <h3>{{ item.value }}</h3>
        <hr>
      </div>
    </div>

    <div class="resume-description">
      <div v-if="item.type === 'description'">
        <p>{{ item.value }}</p>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  inject: ['resumeData'],
}
</script>

<style lang="scss" scoped></style>
