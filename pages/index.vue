<template>
  <top-navbar />
</template>
<script>
import TopNavbar from '@/components/top-navbar'
export default {
  data() {
    return {}
  },
  components: {
    TopNavbar
  },
  created() {
    this.$router.push({
      path: '/jobs'
    })
  }
}
</script>
<style scoped lang="scss"></style>
