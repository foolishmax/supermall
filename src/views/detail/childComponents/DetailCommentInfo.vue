<template>
    <div>hello</div>
</template>
<script>
export default {
  name: "DetailCommentInfo",
  props: {
    commentInfo: {
      type: Object,
      default() {
        return {}
      }
    }
  }
}
</script>
<style scoped></style>
