<template>
  <div class="candidate col-3">
    <div class="box">
      <div class="top d-flex justify-content-between align-items-center">
        <div class="check-box">
          <input type="checkbox" :id="candidate.name.first + candidate.name.last" />
          <label :for="candidate.name.first + candidate.name.last"></label>
        </div>
        <div class="top-candidate">
          <h4 class="text-uppercase">
            Top Candidate
            <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" viewBox="0 0 16 16">
              <path fill="#34CEAC" fill-rule="nonzero" d="M8 0a8 8 0 1 0 0 16A8 8 0 0 0 8 0zm3.233 12.975L8 10.775l-3.233 2.2L5.86 9.221 2.769 6.826l3.908-.121L8 3.025l1.322 3.68 3.908.121-3.091 2.395 1.093 3.754h.001z"/>
            </svg>
          </h4>
        </div>
        <div class="menu">
          <a href="#">
            <svg xmlns="http://www.w3.org/2000/svg" width="4" height="20" viewBox="0 0 4 20">
              <g fill="#C0CCE8" fill-rule="evenodd">
                <circle cx="2" cy="2" r="2"/><circle cx="2" cy="10" r="2"/><circle cx="2" cy="18" r="2"/>
              </g>
            </svg>
          </a>
        </div>
        <!-- /.menu -->

        <!-- /.top-candidate -->
      </div>
      <!-- /.top -->
      <div class="bottom text-center">
        <a href="#">
          <img :src="candidate.picture.medium" class="img-fluid" />
        </a>
        <h3 class="candidate-name">{{ candidate.name.first }} {{ candidate.name.last }}</h3>
        <p class="candidate-rank">{{ candidate.score }}</p>
      </div>
    </div>
    <!-- /.box -->
  </div>
</template>
<script>
  export default {
    name: 'topCandidates',
    props: {
      candidate: Object,
    }
  }
</script>
<style lang="scss" scoped>
  @import "@/assets/styles/common.scss";

  .candidate {
    font-family: "Montserrat", sans-serif;
    .box {
      border-radius: 4px;
      border: solid 1px #e5e9f2;
      background-color: #ffffff;
      padding: 15px 12px 26px;

      .top {
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
        .top-candidate {
          h4 {
            font-size: 12px;
            color: #272b41;
            font-weight: bolder;
            img {
              margin-right: 8px;
            }
          }
        }
        .menu {
          img {
            width: 4px;
            height: 20px;
          }
        }
      }
      .bottom {
        text-align: center;
        a img {
          width: 100px;
          height: 100px;
          border-radius: 50%;
          margin-top: 33px;
        }
        h3.candidate-name {
          font-size: 22px;
          font-weight: bold;
          text-align: center;
          color: #272b41;
          white-space: nowrap;
          width: 12ch;
          margin: 15px auto 0 auto;
          overflow: hidden;
        }
        p.candidate-rank {
          font-size: 60px;
          font-weight: 200;
          text-align: center;
          color: #446694;
          margin-top: 16px;
        }
      }
    }
  }
</style>
