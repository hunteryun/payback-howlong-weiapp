<template>
  <div>
    <van-cell-group v-for="(item, index) in credits" :key="index"  @click.stop>
      <van-cell :title="item.Name" :label="'今日消费还款日: ' + item.DateDetail.CurPay" :border="item.showDetail ? true : false"  @click="clickCell(index)">
        <view slot="right-icon" @click.stop>
          <van-button type="primary" size="small" round @click="clickItem(index)">{{item.DateDetail.IntervalCurPay}} 天</van-button>
        </view>
      </van-cell>
      <van-transition :show="item.showDetail" name="fade-right" >
        <van-cell :border="false">
          <view class="cell-detail">
            <p>当前账单日: {{item.DateDetail.NextBill}} 剩余: {{item.DateDetail.IntervalBill}} 天</p>
            <p>当前还款日: {{item.DateDetail.NextPay}} 剩余: {{item.DateDetail.IntervalPay}} 天</p>
            <p>最长等待期: {{item.DateDetail.WaitDay}} 天</p>
          </view>
        </van-cell>
      </van-transition>
    </van-cell-group>
  </div>
</template>

<script>
export default {
  props: {
    credits: {
      type: Array,
      default: []
    }
  },
  methods: {
    clickItem (index) {
      this.$emit('openPopup', index)
    },
    clickCell (index) {
      if (this.credits[index].showDetail) {
        this.credits[index].showDetail = false
      } else {
        this.$set(this.credits[index], 'showDetail', true)
      }
    }
  }
}
</script>

<style>
.cell-detail {
  text-align: left;
}
</style>
