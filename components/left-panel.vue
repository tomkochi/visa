<template>
  <div class="left-panel">

    <div class="left-nav-item"
         :class="{active: nav === 'search'}">
      <nuxt-link to="" class="d-flex">
        <div class="icon">
          <svg xmlns="http://www.w3.org/2000/svg" width="25" height="22" viewBox="0 0 25 22">
            <path
              d="M9.37,0c6.232,0.116 11.411,7.567 7.988,13.553c-3.479,6.085 -14.888,5.831 -17.073,-2.056c-1.499,-5.414 3.112,-11.534 9.085,-11.497Zm-0.214,2c-4.873,0.091 -8.923,5.799 -6.319,10.485c1.677,3.019 5.656,4.469 8.925,3.297c5.821,-2.087 6.335,-13.619 -2.417,-13.782c-0.095,-0.001 -0.094,-0.001 -0.189,0Z"
              stroke-width="0" fill="#6b739c"/>
            <path d="M14.778,14.513l7.184,6.486" stroke="#6b739c" stroke-width="2"/>
          </svg>
        </div>
        <!-- /.icon -->
        <div class="item-name">SEARCH</div>
        <!-- /.item-name -->
      </nuxt-link to="">
    </div>
    <!-- /.left-nav-item -->

    <div
      class="left-nav-item"
      :class="{active: nav === 'dashboard'}">
      <nuxt-link to="/dashboard" class="d-flex">
        <div class="icon">
          <svg xmlns="http://www.w3.org/2000/svg" width="25" height="22" viewBox="0 0 25 22">
            <path fill="#6B739C" fill-rule="nonzero" stroke="#6B739C" stroke-width=".5"
                  d="M20.595 10.187a.509.509 0 0 0-.237-.278l-7.474-8.732a.506.506 0 0 0-.768 0L1.122 14.023a.509.509 0 0 0 .055.716.505.505 0 0 0 .714-.054l2.307-2.696v6.47A2.54 2.54 0 0 0 6.731 21h11.361a2.54 2.54 0 0 0 2.533-2.54v-6.678l2.484 2.903a.505.505 0 0 0 .714.054.509.509 0 0 0 .055-.716l-3.283-3.836zm-5.68 9.797h-4.83v-3.82a2.42 2.42 0 0 1 2.415-2.42 2.42 2.42 0 0 1 2.414 2.42v3.82zm4.697-1.524c0 .84-.682 1.524-1.52 1.524h-2.165v-3.82a3.436 3.436 0 0 0-3.427-3.437 3.436 3.436 0 0 0-3.427 3.438v3.819H6.73c-.838 0-1.52-.684-1.52-1.524v-7.655L12.5 2.288l7.112 8.31v7.862z"/>
          </svg>
        </div>
        <!-- /.icon -->
        <div class="item-name">HOME</div>
        <!-- /.item-name -->
    </nuxt-link>
    <!-- /.left-nav-item -->
    </div>
    <div
      class="left-nav-item"
      :class="{active: nav === 'jobs'}">
      <nuxt-link to="/jobs" class="d-flex">
        <div class="icon">
          <svg xmlns="http://www.w3.org/2000/svg" width="24" height="22" viewBox="0 0 24 22">
            <path fill="#6B739C" fill-rule="nonzero" stroke="#6B739C" stroke-width=".5"
                  d="M22.989 5.487c0-.664-.53-1.205-1.18-1.205h-6.147V2.663c0-.917-.731-1.663-1.63-1.663H9.969c-.899 0-1.63.746-1.63 1.663v1.62H2.193c-.65 0-1.18.54-1.18 1.202L1 11.213c0 .186.104.356.267.437.25.124.508.238.767.352v7.794c0 .664.53 1.204 1.18 1.204h17.572c.65 0 1.18-.54 1.18-1.204v-7.91c.265-.126.526-.255.781-.392a.485.485 0 0 0 .253-.43l-.011-5.577zM9.287 2.663c0-.383.305-.695.68-.695h4.066c.369 0 .68.318.68.695v1.62H9.288v-1.62zm11.73 17.133a.24.24 0 0 1-.23.236H3.213a.237.237 0 0 1-.231-.236v-7.41c2.064.773 4.37 1.238 6.884 1.38v.671c0 .487.389.883.866.883h2.535a.875.875 0 0 0 .865-.883v-.678c2.547-.158 4.854-.649 6.885-1.462v7.499zm-10.201-5.444v-1.605h2.369v1.605h-2.37zm3.317-1.567v-.123a.875.875 0 0 0-.865-.883h-2.535a.875.875 0 0 0-.866.883v.134c-2.97-.174-5.632-.806-7.918-1.888l.011-5.421c0-.128.107-.237.232-.237H21.81c.126 0 .232.108.232.237l.01 5.283c-2.23 1.147-4.893 1.821-7.918 2.015z"/>
          </svg>
        </div>
        <!-- /.icon -->
        <div class="item-name">JOBS</div>
        <!-- /.item-name -->
      </nuxt-link>
      <div
        v-if="nav === 'jobs'"
        class="sub-items">
        <input type="text" class="jobs-search form-control" placeholder="Jobs">
        <button>Add Job</button>
        <div
          v-for="subItem in subItems.jobs"
          @click="subitemSelected(subItem)"
          :class="{ active: subItem === activeSubItem }"
          class="sub-item">{{ subItem }}</div>
      </div>
      <!-- /.sub-items -->
    </div>
    <!-- /.left-nav-item -->

    <div
      class="left-nav-item"
      :class="{active: nav === 'teams'}">
      <nuxt-link to="/teams" class="d-flex">
        <div class="icon">
          <svg xmlns="http://www.w3.org/2000/svg" width="24" height="22" viewBox="0 0 24 22">
            <g fill="#6B739C" fill-rule="nonzero" stroke="#6B739C" stroke-width=".5">
              <path
                d="M14.297 14.2a3.402 3.402 0 0 0 .843-2.235c0-1.91-1.603-3.465-3.573-3.465s-3.574 1.554-3.574 3.465c0 .827.305 1.616.843 2.234-2.188 1.007-3.605 3.138-3.605 5.548v.409l.408.104a23.99 23.99 0 0 0 5.928.74c2.008 0 4.003-.249 5.928-.74l.428-.111-.02-.468c-.026-2.383-1.437-4.485-3.606-5.482zm-7.955 5.137c.168-2.068 1.602-3.825 3.674-4.446l1.079-.324-.93-.62a2.385 2.385 0 0 1-1.077-1.982c0-1.325 1.112-2.404 2.479-2.404 1.366 0 2.478 1.079 2.478 2.404 0 .791-.402 1.532-1.076 1.981l-.93.621 1.079.324c2.072.621 3.505 2.379 3.673 4.447a23.1 23.1 0 0 1-10.45 0zM19.615 6c-1.866 0-3.384 1.495-3.384 3.333s1.518 3.334 3.384 3.334c1.867 0 3.385-1.496 3.385-3.334S21.482 6 19.615 6zm0 5.585c-1.26 0-2.286-1.01-2.286-2.252 0-1.241 1.026-2.251 2.286-2.251s2.287 1.01 2.287 2.251c0 1.242-1.026 2.252-2.287 2.252zM12 7.667c1.866 0 3.385-1.496 3.385-3.334S13.866 1 12 1c-1.866 0-3.385 1.495-3.385 3.333S10.134 7.667 12 7.667zm0-5.585c1.26 0 2.286 1.01 2.286 2.251 0 1.242-1.025 2.252-2.286 2.252-1.26 0-2.286-1.01-2.286-2.252 0-1.241 1.025-2.251 2.286-2.251zM7.77 9.333C7.77 7.495 6.25 6 4.384 6 2.518 6 1 7.495 1 9.333s1.518 3.334 3.385 3.334c1.866 0 3.384-1.496 3.384-3.334zm-3.385 2.252c-1.26 0-2.287-1.01-2.287-2.252 0-1.241 1.026-2.251 2.287-2.251 1.26 0 2.286 1.01 2.286 2.251 0 1.242-1.026 2.252-2.286 2.252z"/>
            </g>
          </svg>
        </div>
        <!-- /.icon -->
        <div class="item-name">TEAMS</div>
        <!-- /.item-name -->
      </nuxt-link>
    </div>
    <!-- /.left-nav-item -->

    <div
      class="left-nav-item"
      :class="{active: nav === 'contacts'}">
      <nuxt-link to="/contacts" class="d-flex">
        <div class="icon">
          <svg xmlns="http://www.w3.org/2000/svg" width="17" height="20" viewBox="0 0 17 20">
            <path fill="#6B739C" stroke-width="0" fill-rule="nonzero"
                  d="M17 .652A.649.649 0 0 0 16.354 0H1.722a.649.649 0 0 0-.646.652v2.696H0v1.304h1.076v1.696H0v1.304h1.076v1.696H0v1.304h1.076v1.696H0v1.304h1.076v1.696H0v1.304h1.076v2.696c0 .36.289.652.646.652h14.632a.649.649 0 0 0 .646-.652V.652zm-14.633 16h1.098v-1.304H2.367v-1.696h1.098v-1.304H2.367v-1.696h1.098V9.348H2.367V7.652h1.098V6.348H2.367V4.652h1.098V3.348H2.367V1.304h3.594v17.392H2.367v-2.044zm13.342 2.044H7.252V1.304h8.457v17.392z"/>
          </svg>

        </div>
        <!-- /.icon -->
        <div class="item-name">CONTACTS</div>
        <!-- /.item-name -->
      </nuxt-link>
    </div>
    <!-- /.left-nav-item -->

  </div>
</template>
<script>
  import staticData from '~/static/data.json'
  import eventHub from '@/plugins/event-hub'

  export default {
    data() {
      return {
        subItems: {
          jobs: staticData.jobs,
        },
        activeSubItem: staticData.jobs[0],
      }
    },
    methods: {
      subitemSelected (item) {
        this. activeSubItem = item
        eventHub.$emit('subitemSelected', item)
      },
    },
    computed: {
      nav () {
        return this.$route.params.nav.toLowerCase()
      }
    }
  }
</script>
<style scoped lang="scss">
  @import "@/assets/styles/common.scss";

  .left-panel {
    width: 268px;
    .left-nav-item {
      a {
        padding: 18px 33px;
        position: relative;
        &:after {
          content: '';
          position: absolute;
          left: 13px;
          right: 13px;
          bottom: 0;
          height: 1px;
          background: #373c5c;
        }
      }
      .icon {
        margin-right: 25px;
      }
      .item-name {
        font-size: 16px;
        color: #c0cce8;
      }
      .icon path, .item-name {
        -webkit-transition: all 0.3s;
        -moz-transition: all 0.3s;
        -ms-transition: all 0.3s;
        -o-transition: all 0.3s;
        transition: all 0.3s;
      }
      &.active, &:hover {
        .item-name {
          color: #ffffff;
        }
        .icon {
          path {
            fill: #4c84ff;
            stroke: #4c84ff;
          }
        }
      }
      .sub-items {
        background: #1d2032;
        padding: 29px 20px 29px 78px;
        input {
          background: url("../assets/images/search.svg") no-repeat left center;
          -webkit-background-size: 23px;
          background-size: 23px;
          border: none;
          border-bottom: 1px solid #373c5c;
          outline: none;
          margin-bottom: 14px;
          padding: 7px 0 7px 30px;
          width: 100%;
          color: #c0cce8;
          font-size: 18px;
          &:hover,
          &:active,
          &:focus
          {
            outline: 0 !important;
            -webkit-appearance:none;
            box-shadow: none !important;
          }
          &:-ms-input-placeholder,
          &:-moz-placeholder,
          &::-ms-input-placeholder,
          &::-webkit-input-placeholder {
            font-weight: 300;
            color: #6b739c;
          }
        }
        button {
          margin: 14px 0;
          border: none;
          outline: none;
          background: #4c84ff;
          color: #ffffff;
          font-size: 12px;
          padding: 5px 12px;
          -webkit-border-radius: 4px;
          -moz-border-radius: 4px;
          border-radius: 4px;
        }
        .sub-item {
          font-size: 14px;
          font-weight: 300;
          color: #c0cce8;
          padding: 14px 0;
          cursor: pointer;
          -webkit-transition: all 0.3s;
          -moz-transition: all 0.3s;
          -ms-transition: all 0.3s;
          -o-transition: all 0.3s;
          transition: all 0.3s;
          position: relative;
          white-space: nowrap;
          &:hover {
            color: #ffffff;
          }
          &:before {
            content: '';
            position: absolute;
            left: -24px;
            top: 15px;
            width: 10px;
            height: 16px;
            display: block;
            background: url("../assets/images/lp-arrow-right.svg") no-repeat;
            -webkit-background-size: cover;
            background-size: cover;
            -webkit-transition: all 0.3s;
            -moz-transition: all 0.3s;
            -ms-transition: all 0.3s;
            -o-transition: all 0.3s;
            transition: all 0.3s;
            opacity: 0;
          }
          &.active {
            padding-left: 24px;
            color: #ffffff;
            &:before {
              left: 0;
              opacity: 1;
            }
          }
        }
      }
    }
  }
</style>
