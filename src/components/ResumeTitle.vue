<template>
  <div class="resume-title" :key="resumeData.title">
    <h1 v-if="resumeData.title">{{ resumeData.title }}</h1>
  </div>
</template>

<script>
export default {
  props: ['resumeData']
}
</script>
