<template>
  <div class="fitscore-configuration">
    <div class="fit-leadProfile d-flex align-items-center">
      <div class="fit-lead d-flex justify-content-between align-items-center">
        <div
          v-if="pic"
          class="profile-img">
          <img :src="pic" width="40" />
        </div>
        <!-- /.profile-img -->
        <div class="title">
          <h4>{{ title }}</h4>
        </div>
        <!-- /.fit-to -->
        <div
          @click="remove(index)"
          class="close-me d-flex justify-content-center align-items-center">
          <svg xmlns="http://www.w3.org/2000/svg" width="12" height="12" viewBox="0 0 12 12">
            <path fill="#FFF" fill-rule="nonzero" d="M11.657 10.243L7.414 6l4.243-4.243L10.243.343 6 4.586 1.757.343.343 1.757 4.586 6 .343 10.243l1.414 1.414L6 7.414l4.243 4.243z"/>
          </svg>

        </div>
        <!-- /.close -->
      </div>
      <!-- /.fit-lead -->
    </div>
    <!-- /.fit-leadProfile -->
  </div>
  <!-- /.fitscore -->
</template>
<script>
  import eventHub from '@/plugins/event-hub'

  export default {
    name: 'fitscrore',
    props: {
      pic: String,
      title: String,
      index: Number,
    },
    methods: {
      remove (index) {
        eventHub.$emit('removeFsConfig', index)
      }
    }
  };
</script>
<style lang="scss" scoped>
  @import "@/assets/styles/common.scss";

  .fitscore-configuration {
    font-family: "Montserrat", sans-serif;
    margin-bottom: 15px;
    .fit-leadProfile {
      .fit-lead {
        padding: 10px 12px;
        border-radius: 30px;
        background-color: #e5e9f2;
        margin-right: 22px;
        .profile-img img {
          width: 40px;
          height: 40px;
          border-radius: 50%;
          object-fit: cover;
        }
        .title {
          margin: 0 25px;
          h4 {
            font-size: 18px;
            color: #272b41;
            font-weight: bold;
            margin: 0;
          }
        }
        .close-me {
          position: relative;
          width: 40px;
          height: 40px;
          border-radius: 50%;
          background: #c0cce8;
          cursor: pointer;
          -webkit-transition: background-color 0.2s;
          -moz-transition: background-color 0.2s;
          -ms-transition: background-color 0.2s;
          -o-transition: background-color 0.2s;
          transition: background-color 0.2s;
          &:hover {
            background: #fd5e53;
          }
          img {
            position: absolute;
            width: 14px;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            line-height: 36px;
          }
        }
      }
    }
  }
</style>
