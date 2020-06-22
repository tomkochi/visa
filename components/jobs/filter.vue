<template>
  <div class="filter">
    <section id="header" class="d-flex align-items-center justify-content-between">
      <div class="d-flex">
        <svg class="filter-icon" xmlns="http://www.w3.org/2000/svg" width="23" height="22" viewBox="0 0 23 22">
          <g fill="none" fill-rule="evenodd" stroke="#6B739C" stroke-width="2">
            <path d="M3 0v22M20 0v22M11 0v22M0 3h6M17 21h6M8 11h6"/>
          </g>
        </svg>
        <h4>Candidate Filter</h4>
      </div>
      <div @click="closeMe">
        <svg class="close-icon" xmlns="http://www.w3.org/2000/svg" width="12" height="12" viewBox="0 0 12 12">
          <path fill="#6B739C" fill-rule="nonzero" d="M11.957 1.457L10.543.043 6 4.586 1.457.043.043 1.457 4.586 6 .043 10.543l1.414 1.414L6 7.414l4.543 4.543 1.414-1.414L7.414 6z"/>
        </svg>
      </div>
    </section>
    <!-- /#header -->
    <section id="filters" class="d-flex">
      <div class="team-diversity">
        <div class="d-flex align-items-center justify-content-between">
          <h4>team diversity</h4>
          <div class="switch">
            <input type="checkbox" checked id="team-diversity-switch">
            <label for="team-diversity-switch">
              <span class="button"></span>
            </label>
          </div>
        </div>
        <!-- /.team-diversity -->
        <div class="buttons">
          <button
            v-for="d in diversities"
            @click="selectedDiversity = d"
            :class="{ active: selectedDiversity === d }">{{ d }}</button>
        </div>
        <!-- /.buttons -->
      </div>
      <!-- /.team-diversity -->

      <div class="middle">
        <div class="fit-to-team">
          <div class="d-flex align-items-center justify-content-between">
            <h4>fit to team member</h4>
            <div class="switch">
              <input type="checkbox" checked id="fit-to-team-switch">
              <label for="fit-to-team-switch">
                <span class="button"></span>
              </label>
            </div>
          </div>
          <div class="d-flex align-items-center justify-content-between py-5">
            <dropdown-pill
              :pic="`https://randomuser.me/api/portraits/thumb/men/${ Math.floor(Math.random() * 50 + 50) }.jpg`"
              title="Fit to lead"
              :dropdown="['Menu 1', 'Menu 2', 'Menu 3', 'Menu 4']"/>
            <dropdown-pill
              title="Other"
              :dropdown="['Menu 1', 'Menu 2', 'Menu 3', 'Menu 4']"/>
          </div>
        </div>
        <!-- /.fit-to-team -->
        <hr>
        <div class="people">
          <div class="d-flex align-items-center justify-content-between">
            <h4>people</h4>
            <div class="switch">
              <input type="checkbox" id="people">
              <label for="people">
                <span class="button"></span>
              </label>
            </div>
          </div>
          <div class="d-flex align-items-center justify-content-between py-5">
            <dropdown-pill
              title="Perfect Profile"
              :dropdown="['Menu 1', 'Menu 2', 'Menu 3', 'Menu 4']"/>
            <dropdown-pill
              title="Readymade"
              :dropdown="['Menu 1', 'Menu 2', 'Menu 3', 'Menu 4']"/>
          </div>
        </div>
        <!-- /.people -->
      </div>
      <!-- /.middle -->
      <div class="right">
        <div class="problem">
          <div class="d-flex align-items-center justify-content-between">
            <h4>Fix Team’s Problem Area</h4>
            <div class="switch">
              <input type="checkbox" checked id="problem">
              <label for="problem">
                <span class="button"></span>
              </label>
            </div>
          </div>
          <div class="buttons d-flex flex-wrap">
            <button
              v-for="p in problems">{{ p }}</button>
          </div>
          <!-- /.buttons -->
        </div>
        <!-- /.problem -->
        <hr>
        <div class="traits">
          <div class="d-flex align-items-center justify-content-between">
            <h4>Traits</h4>
            <div class="d-flex align-items-center">
              <h4 class="mr-3 c-blue">Bubble View</h4>
              <div class="switch">
                <input type="checkbox" id="traits">
                <label for="traits">
                  <span class="button"></span>
                </label>
              </div>
            </div>
          </div>
          <div class="mt-5">
            <dropdown-pill
              title="Select one"
              :dropdown="['Menu 1', 'Menu 2', 'Menu 3', 'Menu 4']"/>
          </div>
        </div>
        <!-- /.traits -->
      </div>
      <!-- /.right -->
    </section>
    <!-- /#filters -->
  </div>
</template>
<script>
  import DropdownPill from '@/components/jobs/dropdown-pill'

  import eventHub from '@/plugins/event-hub'

  export default {
    data () {
      return {
        selectedDiversity: 'Very Different',
        diversities: [
          'Very Different',
          'Different',
          'Balanced',
          'Very Similar',
          'Similar'
        ],
        problems: [
          'Overall',
          'Efficiency',
          'Respect',
          'Communication',
          'Teamwork',
          'Adaptibility'
        ]
      }
    },
    methods: {
      closeMe () {
        eventHub.$emit('closeFilter')
      }
    },
    components: {
      DropdownPill
    }
  }
</script>
<style scoped lang="scss">
  @import "@/assets/styles/common.scss";

  .filter {
    -webkit-box-shadow: 0 6px 12px 2px rgba(39, 43, 65, 0.32);
    -moz-box-shadow: 0 6px 12px 2px rgba(39, 43, 65, 0.32);
    box-shadow: 0 6px 12px 2px rgba(39, 43, 65, 0.32);
  }
  section#header {
    height: 80px;
    background: #ffffff;
    padding: 30px 40px;
    svg.filter-icon {
      margin-right: 44px;
    }
    h4 {
      font-size: 16px;
      color: #272b41;
      text-transform: uppercase;
    }
    button {
      display: block;
    }
    .close-icon {
      cursor: pointer;
      -webkit-transition: all 0.2s;
      -moz-transition: all 0.2s;
      -ms-transition: all 0.2s;
      -o-transition: all 0.2s;
      transition: all 0.2s;
    }
    &:hover .close-icon {
      -webkit-transform: scale(1.5);
      -moz-transform: scale(1.5);
      -ms-transform: scale(1.5);
      -o-transform: scale(1.5);
      transform: scale(1.5);
    }
  }
  section#filters {
    background: #f5f6fa;
    padding: 26px 40px 45px 40px;
    h4 {
      font-size: 14px;
      color: #272b41;
      text-transform: uppercase;
    }
    .switch {
      input[type=checkbox] {
        -webkit-appearance: none;
        -moz-appearance: none;
        appearance: none;
      }
      label {
        width: 29px;
        height: 16px;
        -webkit-border-radius: 8px;
        -moz-border-radius: 8px;
        border-radius: 8px;
        border: solid 1px #50e3c2;
        background: #c0cce8;
        position: relative;
        -webkit-transform: translateY(5px);
        -moz-transform: translateY(5px);
        -ms-transform: translateY(5px);
        -o-transform: translateY(5px);
        transform: translateY(5px);
        cursor: pointer;
        -webkit-transition: background-color 0.3s;
        -moz-transition: background-color 0.3s;
        -ms-transition: background-color 0.3s;
        -o-transition: background-color 0.3s;
        transition: background-color 0.3s;
        .button {
          position: absolute;
          top: 2px;
          display: inline-block;
          width: 10px;
          height: 10px;
          -webkit-border-radius: 5px;
          -moz-border-radius: 5px;
          border-radius: 5px;
          background: white;
        }
      }
      input + label .button {
        margin-left: 3px;
        -webkit-transition: margin-left 0.3s;
        -moz-transition: margin-left 0.3s, background-color 0.3s;
        -ms-transition: margin-left 0.3s, background-color 0.3s;
        -o-transition: margin-left 0.3s, background-color 0.3s;
        transition: margin-left 0.3s, background-color 0.3s;
        background: #ffffff;
      }
      input:checked + label {
        background: #50e3c2;
      }
      input:checked + label .button {
        margin-left: 14px;
      }
    }

    .team-diversity {
      width: 20%;
      border-right: 1px solid #e5e9f2;
      padding-right : 30px;
      .buttons {
        margin-top: 20px;
        button {
          width: 100%;
          max-width: 193px;
          height: 50px;
          border: 1px solid #c0cce8;
          -webkit-border-radius: 0 25px 25px 0;
          -moz-border-radius: 0 25px 25px 0;
          border-radius: 0 25px 25px 0;
          margin: 6px 0;
          text-align: left;
          padding: 0 22px;
          font-size: 14px;
          color: #272b41;
          background: transparent;
          -webkit-transition: box-shadow 0.2s;
          -moz-transition: box-shadow 0.2s;
          -ms-transition: box-shadow 0.2s;
          -o-transition: box-shadow 0.2s;
          transition: box-shadow 0.2s;
          &:hover {
            -webkit-box-shadow: 5px 4px 9px 0 rgba(192, 204, 232, 0.51);
            -moz-box-shadow: 5px 4px 9px 0 rgba(192, 204, 232, 0.51);
            box-shadow: 5px 4px 9px 0 rgba(192, 204, 232, 0.51);
          }
          &:active,
          &:focus
          {
            outline: 0 !important;
            -webkit-appearance:none;
          }
          &.active {
            background: #ffffff;
            -webkit-box-shadow: 5px 4px 9px 0 rgba(192, 204, 232, 0.51);
            -moz-box-shadow: 5px 4px 9px 0 rgba(192, 204, 232, 0.51);
            box-shadow: 5px 4px 9px 0 rgba(192, 204, 232, 0.51);
          }
        }
      }
    }
    .middle {
      width: 40%;
      padding: 0 30px;
      border-right: 1px solid #e5e9f2;
    }
    .right {
      width: 40%;
      padding: 0 30px;
      .problem {
        .buttons {
          margin-top: 34px;
          button {
            height: 50px;
            border: 1px solid #c0cce8;
            border-radius: 25px;
            background: transparent;
            width: calc(100% / 3 - 12px);
            margin-right: 12px;
            margin-bottom: 12px;
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
          }
        }
      }
      .traits {
        h4.c-blue {
          color: #6b739c;
        }
      }
    }
  }
</style>
