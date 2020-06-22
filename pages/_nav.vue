<template>
  <div>
    <top-navbar/>
    <section id="main" class="d-flex">
      <div class="left-panel">
        <left-panel/>
      </div>
      <!-- /.left-panel -->
      <div class="right-panel">
        <home v-if="nav === 'dashboard'"/>
        <jobs v-if="nav === 'jobs'"/>
        <teams v-if="nav === 'teams'"/>
        <contacts v-if="nav === 'contacts'"/>
      </div>
      <!-- /.right-panel -->
    </section>
    <!-- /#main -->
  </div>
</template>
<script>
  import TopNavbar from '@/components/top-navbar'
  import LeftPanel from '@/components/left-panel'

  export default {
    computed: {
      nav () {
        return this.$route.params.nav.toLowerCase()
      }
    },
    components: {
      LeftPanel,
      TopNavbar,
      Home: () => import('@/components/home'),
      Jobs: () => import('@/components/jobs'),
      Teams: () => import('@/components/teams'),
      Contacts: () => import('@/components/contacts'),
    }
  }
</script>
<style scoped lang="scss">
  section#main {
    width: 100vw;
    height: calc(100vh - 80px);
    overflow: hidden;
    .left-panel {
      background: #272b41;
      overflow-x: hidden;
    }
    .right-panel {
      background: #F5F6FA;
      width: calc(100vw - 268px);
      padding: 45px 30px;
      overflow-y: auto;
      overflow-x: hidden;
    }
  }
</style>
