<template>
  <div class="counter-warp">
    <section class="we-love">
      {{ yoursMood }}
    </section>

    <section class="pics">
      <section
        :key="index"
        class="pics-item"
        @click="toDetail(item)"
        v-for="(item, index) in loveList"
      >
        <img mode="widthFix" class="pics-item__zp" :src="item.imageUrl" />
      </section>
      <section class="pics-add" @click="toEdit">
        +
      </section>
    </section>
  </div>
</template>

<script>
import store from '../../store'
export default {
  data () {
    return {
      disable: true
    }
  },

  computed: {
    yoursMood () {
      return store.state.yoursMood
    },

    loveList () {
      return store.state.loveList
    }
  },

  methods: {
    toDetail (item) {
      if (this.disable) {
        this.disable = false
        store.commit('toDateil', item)
        const url = '../detail/main'
        wx.navigateTo({ url })
      }
    },

    toEdit () {
      if (this.disable) {
        this.disable = false
        const url = '../edit/main'
        wx.navigateTo({ url })
      }
    }
  },

  onLoad () {
    store.commit('getData', {
      url: 'findData',
      params: {},
      successFn: (state) => {
      }
    })
  },

  onShow () {
    this.disable = true
    store.commit('toDateil', {})
  }
}

</script>
<style lang="less">
.counter-warp {
  text-align: center;
}

.we-love {
  font-size: 14px;
  padding-top: 10px;
  padding-bottom: 20px;
}

.pics {
  display: flex;
  padding: 0 10px;
  flex-wrap: wrap;
  flex-direction: column;
  justify-content: center;

  &-add {
    height: 200px;
    font-size: 50px;
    line-height: 200px;
    color: rgba(0, 0, 0, 0.2);
    box-shadow: 0 0 10px rgba(0, 0, 0, 0.2);
  }

  &-item {
    width: 100%;
    height: 200px;
    overflow: hidden;
    margin-bottom: 10px;

    &__zp {
      width: 100%;
      display: block;
      margin-bottom: 10px;
    }
  }
}

</style>
