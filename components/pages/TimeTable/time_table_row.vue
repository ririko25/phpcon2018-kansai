<template>
    <div class="ttrow">
      <div class="ttrow--cdefaults">
        <div class="ttrow--cdefault">
          <div class="ttrow--time" :class="{time_op:!check}">
            <span class="ttrow--time__a" >{{times[0]}}</span>
          </div>
          <div class="ttrow--session__a" :class="{session_op:!check}">
            <time-table-session class="type-a" floor="C01+C02" :session="tracka1" ></time-table-session>
          </div>
          <div class="ttrow--session__b" :class="{session_op:!check}">
            <time-table-session class="type-b" floor="C05" :session="trackb1"></time-table-session>
          </div>
        </div>
        <div class="ttrow--crestrow" v-if="long">
          <div class="ttrow--time__small">
            <span class="ttrow--time__b">{{times[1]}}</span>
          </div>
          <div class="ttrow--timerest">
            <span class="ttrow--timerest__a">15分休憩</span>
          </div>
        </div>
        <div class="ttrow--cdefault" v-if="long">
          <div class="ttrow--time">
            <span class="ttrow--time__a">{{times[2]}}</span>
          </div>
          <div class="ttrow--session__a">
            <time-table-session class="type-a" floor="C01+C02" :session="tracka[1]"></time-table-session>
          </div>
          <div class="ttrow--session__b">
            <time-table-session class="type-b" floor="C05" :session="trackb[1]"></time-table-session>
          </div>
        </div>
      </div>
      <div class="ttrow--clong" v-if="!long" >
        <div class="ttrow--session__c" :class="{session_op:!check}">
          <time-table-session class="type-c" floor="C07" :session="trackc"></time-table-session>
        </div>
      </div>
      <div class="ttrow--clong" v-else>
        <div class="ttrow--session__c is-long">
          <time-table-session class="type-c" floor="C07" :session="trackc"></time-table-session>
        </div>
      </div>
    </div>
</template>

<script>
  import TimeTableSession from "./time_table_session"
    export default {
      props:{
        times: {},
        tracka:{},
        trackb:{},
        trackc:{},
      },
      data() {
          return {
          }
      },
      computed:{
        long(){
          return Array.isArray(this.tracka)
        },
        tracka1(){
          return this.long? this.tracka[0] : this.tracka
        },
        trackb1(){
          return this.long? this.trackb[0] : this.trackb
        },
        check(){
            return this.tracka1.name
        }
      },
      components:{
        TimeTableSession
      }
    }

</script>

<style lang="scss" scoped>
    @import "~assets/scss/library/_variable.scss";
    @import "~assets/scss/library/_mixin.scss";

    $baseWidth: 30%; // それぞれのトラックの幅
    $baseHeight: 290px; // それぞれのトラックの高さ
    $restHeight: 30px; // それぞれのトラックの高さ
    $ttrow-gutter: 10px; // 時間ごとの盾のガッター

    $longHeight: 100%;


.ttrow{
  color: $clr_baseDark;
  display: flex;
  margin: $ttrow-gutter 0;

  @include desktop{
    margin: 4px 0;
  }

  &--cdefaults{
    width: 100 - $baseWidth;
  }
  &--cdefault{
    display: flex;
  }
  &--crestrow{
    display: flex;
    margin: $ttrow-gutter 0;
    height: $restHeight;
    @include desktop {
      margin: 4px 0 ;
    }

    .ttrow--time{
      writing-mode: horizontal-tb;
      overflow: visible;
    }
  }
  &--session__a,
  &--session__b,
  &--session__c{
    height: $baseHeight;
    @include desktop {
      height: 200px;
    }
  }
  .session_op {
    height:60px;
  }
  &--session__a,
  &--session__b{
    width: $baseWidth * 10 /7;
    @include desktop() {
      margin: 0 2px;
    }
  }
  &--session__c{
    width: 100%; // abc で幅を考えない
  }
  &--session__c.is-long{
    width: 100%; // abc で幅を考えない
    height: $longHeight;
  }
  &--time {
    padding: 8px 0;
    width: 100-($baseWidth * 10 /7)*2;
    background: #f7f7f7;
    writing-mode: vertical-rl;
    text-align: left;
    z-index: 1;
    position: relative;
    @include desktop() {
      padding: 0;
      writing-mode: horizontal-tb;
      margin: 0 2px;
    }
    &__a {
      font-size: 1.3rem;
      position: absolute;
      right: 50%;
      transform: translate(50%, 0);
      @include desktop() {
        font-size: 1.6rem;
        left: 50%;
        right: auto;
        padding: 0;
        transform: translate(-50%, 50%);
      }
    }
    &__b {
      font-size: 1.3rem;
      position: absolute;
      top: 50%;
      left: 50%;
      transform: translate(0, -50%);
      @include desktop() {
        font-size: 1.6rem;
        transform: translate(-25%, -50%);
      }
    }
  }
  &--time__small {
    width: 100-($baseWidth * 10 /7)*2;
    background: #f7f7f7;
    text-align: left;
    z-index: 1;
    position: relative;
    @include desktop() {
    }
  }
  &--timerest{
    background: #f7f7f7;
    width: 100%;
    position: relative;
    @include desktop() {
      margin-right: 2px;
    }
    &__a {
      font-weight: bold;
      position: absolute;
      top: 50%;
      left: 50%;
      transform: translate(-50%, -50%);
    }
  }
  &--timerestCommon{
    background: #f7f7f7;
    width: 100%;
    position: relative;
    @include desktop() {
      margin-right: 2px;
    }
    &__a {
      font-weight: bold;
      position: absolute;
      top: 50%;
      left: 50%;
      transform: translate(-50%, -50%);
    }
  }
  &--clong{
    width: $baseWidth;
    @include desktop() {
      margin: 0 2px;
    }
  }
}

</style>
