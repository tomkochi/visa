<template>
  <div class="pill d-flex align-items-center justify-content-between">
    <div>
      <img v-if="pic" :src="pic" width="40" height="40" class="rounded-circle" alt="">
    </div>
    <div class="title w-100">{{ title }}</div>
    <div
      v-outside-click="{
        exclude: ['dropdown'],
        handler: 'hideDropdown'
      }">
      <div
        class="dropdown-arrow d-flex justify-content-center align-items-center">
        <svg xmlns="http://www.w3.org/2000/svg" width="16" height="10" viewBox="0 0 16 10">
          <path fill="#6B739C" fill-rule="nonzero" d="M16 1.5l-1-1-7 7-7-7-1 1 8 8z"/>
        </svg>
      </div>
      <!-- /.dropdown-arrow -->
    </div>
    <ul
      ref="dropdown"
      v-show="showDropdown && dropdown"
      class="list-unstyled dropdown">
      <li
        v-for="item in dropdown"
        class="menu-item">{{ item }}</li>
    </ul>
    <!-- /.dropdown -->
  </div>
</template>
<script>
  let handleOutsideClick
  export default {
    name: 'dropdown-pill',
    props: {
      pic: String,
      title: String,
      dropdown: Array
    },
    data() {
      return {
        showDropdown: false
      }
    },
    methods: {
      hideDropdown () {
        this.showDropdown = false
      }
    }
  }
</script>
<style scoped lang="scss">
  @import "@/assets/styles/common.scss";

  .pill {
    position: relative;
    height: 60px;
    width: calc(50% - 12px);
    border: 1px solid #e5e9f2;
    -webkit-border-radius: 30px;
    -moz-border-radius: 30px;
    border-radius: 30px;
    padding-left: 12px;
    padding-right: 24px;
    background: transparent;
    -webkit-transition: all 0.2s;
    -moz-transition: all 0.2s;
    -ms-transition: all 0.2s;
    -o-transition: all 0.2s;
    transition: all 0.2s;
    &:hover {
      background: #ffffff;
      -webkit-box-shadow: 5px 4px 9px 0 rgba(192, 204, 232, 0.51);
      -moz-box-shadow: 5px 4px 9px 0 rgba(192, 204, 232, 0.51);
      box-shadow: 5px 4px 9px 0 rgba(192, 204, 232, 0.51);
    }
    .title {
      padding-right: 12px;
      text-align: center;
      white-space: nowrap;
    }
    .dropdown-arrow {
      width: 30px;
      height: 30px;
      -webkit-border-radius: 15px;
      -moz-border-radius: 15px;
      border-radius: 15px;
      background: transparent;
      cursor: pointer;
      -webkit-transition: background-color 0.2s;
      -moz-transition: background-color 0.2s;
      -ms-transition: background-color 0.2s;
      -o-transition: background-color 0.2s;
      transition: background-color 0.2s;
      &:hover {
        background: #e2e2e2;
      }
    }
    .dropdown {
      position: absolute;
      right: 0;
      top: 0;
    }
  }
</style>
