<template>
  <section>
    <div>
      <div class="p-job_header">
        <router-link
          to="/">
          <img src="~assets/images/logo.svg" class="p-job_logo" alt="Scala Kansai summit2018">
        </router-link>
      </div>
      <div class="p-job">
        <div class="c-container">
          <h3 class="p-job_heading">
            求人・広告
          </h3>
          <div class="p-job_read">
            Scala関西Summitはスポンサーの皆様からの支援を頂いて運営しています。
          </div>
          <div class="p-job_platinum" v-if="sponsors.platinum">
            <div class="title">
              Platinum
            </div>
            <div>
              <div class="list" v-for="sponsor in sponsors.platinum" :key="sponsor.name" v-if="sponsor.job" :id="sponsor.name">
                <div class="listItem">
                  <div class="rank">
                  </div>
                  <div class="rankText">
                    <p>Platinum</p>
                    <i class="fa fa-star"></i>
                  </div>
                  <div class="inner">
                    <a :href="sponsor.url" class="company" target="_blank">{{sponsor.name}}</a>
                    <span class="subtitle">{{sponsor.job.title}}</span>
                    <a :href="sponsor.url" class="logoLink" target="_blank"><div class="logo" :style="logoStyle(sponsor)" /></a>
                    <div class="description" v-html="md(sponsor.job.message)" />
                    <div class="linkArea">
                      <a :href="sponsor.job.url" class="btn" target="_blank"><i class="fas fa-external-link-alt"></i>{{ sponsor.job.buttonTitle || "広告・求人ページ" }}</a>
                    </div>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="p-job_gold" v-if="sponsors.gold">
            <div class="title">
              Gold
            </div>
            <div class="list" v-for="sponsor in sponsors.gold" :key="sponsor.name" v-if="sponsor.job" :id="sponsor.name">
              <div class="listItem">
                <div class="rank">
                </div>
                <div class="rankText">
                  <p>Gold</p>
                  <i class="fa fa-star"></i>
                </div>
                <div class="inner">
                  <a :href="sponsor.url" class="company" target="_blank">{{sponsor.name}}</a>
                  <span class="subtitle">{{sponsor.job.title}}</span>
                  <a :href="sponsor.url" class="logoLink" target="_blank"><div class="logo" :style="logoStyle(sponsor)" /></a>
                  <div class="description" v-html="md(sponsor.job.message)" />
                  <div class="linkArea">
                    <a :href="sponsor.job.url" class="btn" target="_blank"><i class="fas fa-external-link-alt"></i>{{ sponsor.job.buttonTitle || "広告・求人ページ" }}</a>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="p-job_silver" v-if="sponsors.silver">
            <div class="title">
              Silver
            </div>
            <div class="list" v-for="sponsor in sponsors.silver" :key="sponsor.name" v-if="sponsor.job" :id="sponsor.name">
              <div class="listItem">
                <div class="rank">
                </div>
                <div class="rankText">
                  <p>Silver</p>
                  <i class="fa fa-star"></i>
                </div>
                <div class="inner">
                  <a :href="sponsor.url" class="company" target="_blank">{{sponsor.name}}</a>
                  <div class="row">
                    <div class="col-sm-4">
                      <a :href="sponsor.url" class="logoLink" target="_blank"><div class="logo" :style="logoStyle(sponsor)" /></a>
                    </div>
                    <div class="col-sm">
                      <div class="description" v-html="md(sponsor.job.message)" />
                    </div>
                  </div>
                  <div class="linkArea">
                    <a :href="sponsor.job.url" class="btn" target="_blank"><i class="fas fa-external-link-alt"></i>{{ sponsor.job.buttonTitle || "広告・求人ページ" }}</a>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="p-job_wanted">
            <p>スポンサー随時受付中です！</p>
            <div>
              <a href="https://docs.google.com/forms/d/e/1FAIpQLSdEdPzvXlaB7RfeaqmIy4hPpGlhz-I8ciNw-QNws7S150gHgg/viewform?usp=sf_link" target="_blank" class="p-job_btn-wanted">
                <i class="fas fa-star"></i>
                スポンサー申込み
              </a>
            </div>
            <div>
              <router-link
                to="/"
                class="p-job_btn-top">
                <i class="fas fa-chevron-left"></i>
                TOPに戻る
              </router-link>
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script>
import marked from "marked"

export default {
  computed:{
    sponsors(){
      return this.$store.state.sponsors
    },
  },
  methods:{
    logoStyle (sponsor){
      return {
        backgroundImage: `url('/sponsors/${sponsor.image}')`
      }
    },
    md (string) {
      return marked(string);
    }
  },
}
</script>

<style lang="scss" scoped>
  @import "~/assets/scss/library/_variable.scss";
  @import "~/assets/scss/library/_mixin.scss";

  .p-job {
    @include secPadding;
    background: $clr_bg-orange;

    &_header {
      background: white;
    }
    &_logo {
      padding: 10px;
      width: 75%;
      max-width: 150px;
      @include desktop {
        padding: 20px;
        width: 60%;
        max-width: 300px;
      }
    }

    &_heading {
      @include secHeading;
    }

    &_read {
      @include secRead;
    }

    /* 共通クラス */

    .title {
      @include title-border;
    }
    .row {
      justify-content: flex-start;
    }


    .list {
      box-sizing: border-box;
      text-align: center;
    }

    .listItem {
      margin-bottom: 40px;
      box-sizing: border-box;
      padding: 40px 0 0;
      text-align: center;
      background: white;
      position: relative;

      @include desktop {
        padding: 50px 0 0;
      }

      .inner {
        width: 100%;
        margin: 0 auto 30px;
        padding: 0 20px;
        display: inline-block;
        text-align: left;
        box-sizing: border-box;

        @include desktop {
          margin: 0 auto 60px;
        }
      }

      .company {
        display: block;
        padding-bottom: .1em;
        width: 100%;
        text-align: left;
        font-size: 2rem;
        font-weight: bold;
        color: $clr_brown;
      }
      .subtitle {
        display: inline-block;
        margin-bottom: 20px;
        font-size: 1.4rem;
        color: $clr_brown;
      }

      .rank {
        border-top: 45px solid #5CC5B8;
        border-bottom: 45px solid transparent;
        border-left: 45px solid transparent;
        border-right: 45px solid #5CC5B8;
        position: absolute;
        top :0;
        right :0;

        @include desktop {
          border-top: 55px solid #5CC5B8;
          border-bottom: 55px solid transparent;
          border-left: 55px solid transparent;
          border-right: 55px solid #5CC5B8;
        }
      }
      .rankText {
        display: inline-block;
        color: white;
        position: absolute;
        letter-spacing: 1px;
        top : 4px;
        right: 4px;
        text-align: center;
        @include desktop {
          top : 8px;
          right :8px;
        }

        p {
          margin: 0;
          font-size: 1.1rem;
          @include desktop {
            font-size: 1.4rem;
          }
        }
        i {
          font-size: 1.4rem;
          @include desktop {
            font-size: 2rem;
          }
        }
      }

      .linkArea {
        text-align: center;
      }
      .description {
        margin-bottom: 40px;
        /deep/ a {
          color: #C95F1C;
          text-decoration: underline;
        }
      }

      .btn {
        @include btnIcon;
      }
    }

    /* プラチナ */

    &_platinum {
      margin-bottom: 30px;
      @include desktop {
        margin-bottom: 60px;
      }

      @include desktop {

      }
      .row {
        justify-content: center;
      }
      .listItem {
        .inner {
          max-width: 750px;
        }
        .logoLink {
          display: inline-block;
          width: 100%;
          text-align: center;
        }
        .logo {
          margin:  0 auto;
          display: inline-block;
          margin-bottom: 15px;
          width: 100%;
          max-width: 600px;
          background-image: url("http://placehold.it/600x480");
          background-repeat: no-repeat;
          background-size: contain;
          background-position: center;

          &::before {
            content: "";
            display: block;
            padding-top: 80%;
          }
        }

        .description {
          display: block;
          width: 100%;
          box-sizing: border-box;

        }

      }
    }

    /* ゴールド */

    &_gold {
      margin-bottom: 30px;
      @include desktop {
        margin-bottom: 60px;
      }

      .list {

      }
      .listItem {
        .rank {
          border-top: 40px solid #F7B444;
          border-bottom: 40px solid transparent;
          border-left: 40px solid transparent;
          border-right: 40px solid #F7B444;
          @include desktop {
            border-top: 50px solid #F7B444;
            border-bottom: 50px solid transparent;
            border-left: 50px solid transparent;
            border-right: 50px solid #F7B444;
          }
        }
        .inner {
          max-width: 100%;
          @include desktop {
            max-width: 750px;
          }
        }
        .logo {
          display: block;
          margin: 0 auto;
          margin-bottom: 15px;
          width: 100%;
          max-width: 250px;
          background-image: url("http://placehold.it/300x240");
          background-repeat: no-repeat;
          background-size: contain;
          background-position: center;

          @include desktop {
            max-width: 350px;
          }

          &::before {
            content: "";
            display: block;
            padding-top: 80%;
          }
        }
      }
    }

    /* シルバー */

    &_silver {
      .listItem {
        .rank {
          border-top: 40px solid #BDB5A9;
          border-bottom: 40px solid transparent;
          border-left: 40px solid transparent;
          border-right: 40px solid #BDB5A9;
          @include desktop {
            border-top: 50px solid #BDB5A9;
            border-bottom: 50px solid transparent;
            border-left: 50px solid transparent;
            border-right: 50px solid #BDB5A9;
          }
        }
        .inner {
          max-width: 100%;
          @include desktop {
            max-width: 750px;
          }
        }
        .logo {
          display: block;
          margin: 0 auto;
          width: 100%;
          max-width: 160px;
          background-image: url("http://placehold.it/200x160");
          background-repeat: no-repeat;
          background-size: contain;
          background-position: center;
          @include desktop {
            margin: 0;
            background-position: left;
          }

          @include desktop {
            max-width: 200px;
          }

          &::before {
            content: "";
            display: block;
            padding-top: 80%;
          }
        }
        .description {
          @include desktop {
            margin-top: 0;
          }
        }

      }
    }
    &_wanted {
      margin-top: 40px;
      font-size: 1.8rem;
    }
    &_btn-wanted {
      @include btnIcon();
      margin-bottom: 50px;

    }
    &_btn-top {
      @include btnIcon(white,$clr_brown);
    }
  }
</style>
