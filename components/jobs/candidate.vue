<template>
  <div class="candidate d-flex align-items-center">
    <div class="left d-flex align-items-center">
      <div class="check-box">
        <input type="checkbox" :id="candidate.name.first + candidate.name.last" />
        <label :for="candidate.name.first + candidate.name.last"></label>
      </div>
      <!-- /.check-box -->
      <div>
        <div
          :class="{ eligible: candidate.eligible }"
          class="candidate-pic">
          <img :src="candidate.picture.thumbnail" class="img-fluid" width="40" height="40" />
        </div>
        <!-- /.candidate-pic -->
      </div>
      <div class="candidate-name">
        <h4>{{ candidate.name.first }} {{ candidate.name.last }}</h4>
      </div>
      <!-- /.candidate-name -->
    </div>
    <!-- /.d-flex -->
    <div class="candidate-nature">
      <h4>{{ candidate.nature }}</h4>
    </div>
    <!-- /.candidate-nature -->
    <div class="right d-flex align-items-center">
      <div class="candidate-score">
        <p>{{ candidate.score }}</p>
      </div>
      <!-- /.candidate-score -->
      <div class="menu">
        <svg xmlns="http://www.w3.org/2000/svg" width="4" height="20" viewBox="0 0 4 20">
          <g fill="#C0CCE8" fill-rule="evenodd">
            <circle cx="2" cy="2" r="2"/><circle cx="2" cy="10" r="2"/><circle cx="2" cy="18" r="2"/>
          </g>
        </svg>
      </div>
      <!-- /.menu -->
    </div>
    <!-- /.right -->
  </div>
  <!-- /.candidate -->
</template>
<script>
  export default {
    name: 'candidate',
    props: {
      candidate: Object
    }
  }
</script>
<style lang="scss" scoped>
  @import "@/assets/styles/common.scss";

  .left {
    width: 30%;
  }
  .candidate-nature {
    width: 60%;
  }
  .right {
    width: 10%;
  }
  .left {
    .check-box {
      margin-right: 34px;
      input[type="checkbox"] {
        display: none;
        cursor: pointer;
        position: relative;
      }
      input + label {
        position: relative;
      }
      label {
        font-size: 18px;
        color: #747474;
        cursor: pointer;
        white-space: nowrap;
        display: inline-block;
      }
      input + label::before {
        position: absolute;
        content: "";
        width: 15px;
        height: 15px;
        left: 0;
        top: -10px;
        background: url("../../assets/images/unchecked.svg");
        background-size: cover;
        transition: all 0.2s;
      }
      input:checked + label::before {
        background: url("../../assets/images/checked.svg");
      }
    }
    .candidate-pic {
      margin-right: 34px;
      position: relative;
      width: 40px;
      height: 40px;
      border-radius: 20px;
      overflow: hidden;
      &.eligible {
        &:after {
          content: "";
          width: 16px;
          height: 16px;
          position: absolute;
          background-image: url("../../assets/images/star.svg");
          right: -9px;
          top: 0;
        }
      }
    }
    .candidate-name h4 {
      font-size: 18px;
      font-weight: 300;
      color: #272b41;
      text-transform: capitalize;
      margin: 0;
    }
  }
  .candidate-nature h4 {
    text-align: center;
    font-size: 18px;
    font-weight: 300;
    color: #6b739c;
    text-transform: capitalize;
    margin: 0;
  }
  .right {
    .candidate-score {
      p {
        font-size: 18px;
        font-weight: 300;
        color: #446694;
        margin: 0 72px 0 0;
      }
    }
    .menu {
      width: 4px;
      height: 20px;
    }
  }
</style>
