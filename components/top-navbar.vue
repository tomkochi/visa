<template>
  <div>
    <b-navbar toggleable="lg" type="light" variant="white" class="shadow-sm" fixed="top">
      <b-navbar-brand href="#">
        <img src="~/assets/images/visa.svg" height="21" alt="">
      </b-navbar-brand>

      <b-navbar-toggle target="nav-collapse"></b-navbar-toggle>

      <b-collapse id="nav-collapse" is-nav>
        <!-- Right aligned nav items -->
        <b-navbar-nav class="ml-auto">
          <b-navbar-nav>
            <b-nav-item href="#">
              <img src="~/assets/images/profiles/05.jpg" width="40" class="rounded" alt="">
            </b-nav-item>
          </b-navbar-nav>
        </b-navbar-nav>
      </b-collapse>
    </b-navbar>
    <div class="navbar-spacer"></div>
  </div>
</template>
<script></script>
<style scoped lang="scss">
  @import "@/assets/styles/common.scss";

  nav {
    height: 80px;
  }
  .navbar-spacer {
    height: 80px;
  }
</style>
