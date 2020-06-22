<template>
  <div>
    <header>
      <div class="d-flex justify-content-between align-items-center">
        <div class="header job-title">
          <div>
            <div class="section-title">Job Title</div>
            <div class="value">{{ job }}</div>
          </div>
        </div>
        <!-- /.header -->
        <div class="d-flex">
          <div class="header candidates">
            <div>
              <div class="section-title">Candidates</div>
              <div class="value">{{ candidates ? candidates.length : 0 }}</div>
            </div>
          </div>
          <!-- /.header -->
          <div class="header incomplete">
            <div>
              <div class="section-title">Incomplete</div>
              <div class="value">{{ Math.floor(Math.random() * 10 + 1) }}</div>
            </div>
          </div>
          <!-- /.header -->
          <div class="header edit">
            <div>
              <svg xmlns="http://www.w3.org/2000/svg" width="23" height="23" viewBox="0 0 23 23">
                <path
                  fill="#6B739C"
                  fill-rule="nonzero"
                  d="M1.354 15.921L0 22.689l6.768-1.354L22.689 5.414 17.275 0 1.354 15.921zm4.428 3.572l-3.232.646.646-3.232L14.275 5.828l2.586 2.586L5.782 19.493zM18.275 7l-2.586-2.586 1.586-1.586 2.586 2.586L18.275 7z"
                />
              </svg>
            </div>
          </div>
          <!-- /.header -->
        </div>
        <!-- /.d-flex -->
      </div>
    </header>

    <section id="search" class="d-flex align-items-center">
      <input type="text" class="form-control mr-4" placeholder="Enter name" />
      <button class="d-flex">
        <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" viewBox="0 0 16 16">
          <path
            fill="#FFF"
            fill-rule="nonzero"
            d="M8 0a8 8 0 1 0 0 16A8 8 0 0 0 8 0zm0 14A6 6 0 1 1 8 2a6 6 0 0 1 0 12zm4-5H9v3H7V9H4V7h3V4h2v3h3v2z"
          />
        </svg>
        <span class="ml-2">ADD CANDIDATE</span>
      </button>
    </section>
    <!-- /#search -->
    <section v-if="showFitToLead || pillTitles.length" id="fs-config">
      <div class="section-title mb-3">Fitscore Configuration</div>
      <div class="d-flex justify-content-between">
        <div class="left d-flex">
          <div v-if="candidates" class="fs-pills d-flex flex-wrap">
            <fs-pill
              v-if="showFitToLead"
              :pic="candidates[20].picture.thumbnail"
              :index="-1"
              title="Fit to Lead"
            />
            <fs-pill v-for="(title, i) in pillTitles" :key="i" :index="i" :title="title" />
          </div>
          <!-- /.fitscore-pill -->
          <div>
            <div
              @click="showFilter = true"
              class="fs-filter d-flex justify-content-center align-items-center"
            >
              <svg xmlns="http://www.w3.org/2000/svg" width="23" height="22" viewBox="0 0 23 22">
                <g fill="none" fill-rule="evenodd" stroke="#FFF" stroke-width="2">
                  <path d="M3 0v22M20 0v22M11 0v22M0 3h6M17 21h6M8 11h6" />
                </g>
              </svg>
            </div>
            <!-- /.filter -->
          </div>
        </div>
        <!-- /.left -->
        <div class="right">
          <div class="fs-menu d-flex justify-content-center align-items-center">
            <svg xmlns="http://www.w3.org/2000/svg" width="29" height="24" viewBox="0 0 29 24">
              <g fill="none" fill-rule="evenodd" stroke="#6B739C" stroke-width="2">
                <path
                  d="M0 1h2.64M7.04 1h21.12M0 11.56h2.64M7.04 11.56h21.12M0 22.12h2.64M7.04 22.12h21.12"
                />
              </g>
            </svg>
          </div>
          <!-- /.menu -->
        </div>
        <!-- /.right -->
      </div>
    </section>
    <!-- /#fitscore-configuration -->
    <section id="top-candidates">
      <div class="row">
        <top-candidate v-if="candidates" v-for="c in 4" :candidate="candidates[c - 1]" :key="c" />
      </div>
      <!-- /.row -->
    </section>
    <!-- /#top-candidates -->

    <section id="all-calldidates">
      <div class="section-title mb-3">
        All candidates
        <span>|</span>
        {{ start + 1 }}-{{ end + 1 }}
      </div>
      <div class="candidates">
        <candidate
          v-if="candidates && c < candidates.length"
          v-for="c in range"
          :candidate="candidates[c]"
          :key="c"
          class="candidate"
        />
      </div>
      <!-- /.candidates -->
    </section>
    <!-- /#all-calldidates -->

    <div v-observe-visibility="loadMore" />

    <transition name="fade">
      <section @click.self="showFilter = false" v-if="showFilter" id="filter">
        <candidate-filter />
      </section>
      <!-- /#filter -->
    </transition>
  </div>
</template>
<script>
import staticData from '~/static/data.json'

import FsPill from '@/components/jobs/fs-pill'
import TopCandidate from '@/components/jobs/top-candidate'
import Candidate from '@/components/jobs/candidate'
import CandidateFilter from '@/components/jobs/filter'

import axios from 'axios'
import eventHub from '@/plugins/event-hub'

import Vue from 'vue'
import { ObserveVisibility } from 'vue-observe-visibility'

Vue.directive('observe-visibility', ObserveVisibility)

export default {
  data() {
    return {
      job: staticData.jobs[0],
      pillTitles: staticData.pillTitles,
      nature: staticData.nature,
      candidates: null,
      showFitToLead: true,
      start: 4,
      end: 13,
      showFilter: false
    }
  },
  created() {
    let records = Math.floor(Math.random() * 20 + 80)
    axios({
      method: 'get',
      url: `https://randomuser.me/api/?results=${records}&inc=name,picture,id&noinfo`
    }).then(results => {
      this.candidates = results.data.results
      this.candidates = this.candidates.map(c => {
        c.score = Math.floor(Math.random() * 60 + 30)
        c.nature = this.nature[Math.floor(Math.random() * 4)]
        c.eligible = Math.random() >= 0.5
        return c
      })
      this.candidates.sort((a, b) => {
        return b.score - a.score
      })
      console.log(this.candidates[0])
    })
  },
  mounted() {
    eventHub.$on('removeFsConfig', index => {
      if (index === -1) {
        this.showFitToLead = false
      } else {
        this.pillTitles.splice(index, 1)
      }
    })
    eventHub.$on('closeFilter', () => {
      this.showFilter = false
    })
    eventHub.$on('subitemSelected', item => {
      this.job = item
    })
  },
  methods: {
    loadMore(visible, entry) {
      if (!visible || !this.candidates) return false
      if (this.end < this.candidates.length) {
        this.end += 10
      }
    }
  },
  computed: {
    range() {
      let arr = []
      for (let i = this.start; i <= this.end; i++) {
        arr.push(i)
      }
      return arr
    }
  },
  components: {
    FsPill,
    TopCandidate,
    Candidate,
    CandidateFilter
  }
}
</script>
<style scoped lang="scss">
@import '@/assets/styles/common.scss';

.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.5s;
}
.fade-enter, .fade-leave-to /* .fade-leave-active below version 2.1.8 */ {
  opacity: 0;
}
.section-title {
  font-size: 12px;
  color: #272b41;
  text-transform: uppercase;
}
header {
  .job-title {
    .value {
      font-size: 30px;
      color: #272b41;
    }
  }
  .candidates {
    padding: 0 80px;
    .value {
      font-size: 30px;
      color: #446694;
    }
  }
  .incomplete {
    padding: 0 80px;
    .value {
      font-size: 30px;
      color: #91cded;
    }
  }
  .edit {
    padding: 0 40px;
    div {
      width: 40px;
      height: 40px;
      -webkit-border-radius: 50%;
      -moz-border-radius: 50%;
      border-radius: 50%;
      background: #ffffff;
    }
    svg {
      margin-left: 10px;
      margin-top: 10px;
    }
  }
  .job-title,
  .candidates,
  .incomplete,
  .edit {
    height: 88px;
    border-left: 1px solid #c0cce8;
    display: flex;
    align-items: center;
  }
  .job-title {
    border: none;
  }
}
section#search {
  margin: 32px 0;
  input {
    height: 60px;
    font-size: 22px;
    font-weight: 300;
    color: #272b41;
    border-radius: 4px;
    box-shadow: -4px 4px 9px 0 rgba(192, 204, 232, 0.17);
    border: solid 1px #e5e9f2;
    background: url('../assets/images/search.svg') #ffffff;
    background-repeat: no-repeat;
    background-position: 22px 18px;
    -webkit-background-size: 30px;
    background-size: 30px;
    padding-left: 60px;
    &:-ms-input-placeholder,
    &:-moz-placeholder,
    &::-ms-input-placeholder,
    &::-webkit-input-placeholder {
      font-weight: 300;
      color: #6b739c;
    }
  }
  button {
    height: 45px;
    border-radius: 4px;
    box-shadow: -3px 5px 9px 0 rgba(76, 132, 255, 0.49);
    background-color: #4c84ff;
    font-size: 12px;
    font-weight: 600;
    color: #ffffff;
    white-space: nowrap;
    padding: 11px 14px;
  }
}
section#fs-config {
  .fs-filter {
    position: relative;
    width: 60px;
    height: 60px;
    -webkit-box-shadow: -3px 5px 9px 0 rgba(255, 128, 76, 0.31);
    -moz-box-shadow: -3px 5px 9px 0 rgba(255, 128, 76, 0.31);
    box-shadow: -3px 5px 9px 0 rgba(255, 128, 76, 0.31);
    background-color: #ff804c;
    border-radius: 50%;
    margin-right: 30px;
    cursor: pointer;
    border: 1px solid transparent;
    -webkit-transition: border-color 0.2s;
    -moz-transition: border-color 0.2s;
    -ms-transition: border-color 0.2s;
    -o-transition: border-color 0.2s;
    transition: border-color 0.2s;
    &:hover {
      border: 1px solid #fff;
    }
    img {
      position: absolute;
      width: 23px;
      top: 50%;
      left: 50%;
      transform: translate(-50%, -50%);
      line-height: 36px;
    }
  }
  .fs-menu {
    position: relative;
    width: 60px;
    height: 60px;
    border-radius: 4px;
    box-shadow: -4px 4px 9px 0 rgba(192, 204, 232, 0.17);
    border: solid 1px #e5e9f2;
    background-color: #ffffff;
    img {
      position: absolute;
      top: 50%;
      left: 50%;
      transform: translate(-50%, -50%);
      line-height: 36px;
    }
  }
}
section#top-candidates {
  margin-top: 30px;
}
section#all-calldidates {
  margin-top: 30px;
  .candidates {
    -webkit-border-radius: 4px;
    -moz-border-radius: 4px;
    border-radius: 4px;
    border: 1px solid #e5e9f2;
    background: #ffffff;
    padding: 7px 17px;
    .candidate {
      margin: 15px 0;
      position: relative;
      &:not(:last-of-type):after {
        content: '';
        position: absolute;
        left: 0;
        bottom: -8px;
        width: 100%;
        height: 1px;
        background: #e5e9f2;
      }
    }
  }
}
section#filter {
  position: fixed;
  left: 0;
  top: 0;
  right: 0;
  bottom: 0;
  background: rgba(39, 43, 65, 0.46);
  /*background: #ffffff;*/
  z-index: 2000;
}
</style>
