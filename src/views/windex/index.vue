<template lang="pug">
  el-container()
    el-header(style="height:100px;width:100%")
      navbar()
      //- div.demo-input-suffix
      //-   el-input(
      //-     style="width:400px;height:80px;line-hieght:80px;",
      //-     placeholder="搜索模型、图片",
      //-     suffix-icon="el-icon-search",
      //-     v-model="searchKey"
      //-   )
    el-container()
      el-aside(style="width:200px;display:flx;align-items:center;justify-content:center;")
        el-tabs(tab-position="left", style="height: 200px;")
          el-tab-pane(label="模型广场")
          el-tab-pane(label="精美图片")
      el-main(style="height:1000px;")
        //- vue-waterfall-easy(
          ref="waterfall",
          :imgsArr="imgsArr",
          @scrollReachBottom="getData",
          @click="clickFn",
          @imgError="imgErrorFn",
          :enablePullDownEvent="true",
          @pullDownMove="pullDownMove",
          @pullDownEnd="pullDownEnd")
        vue-waterfall-easy(
          ref="waterfall",
          :imgsArr="imgsArr",
          @scrollReachBottom="getData",
          @click="clickFn",
          @imgError="imgErrorFn")

          .img-info(slot-scope="props")
            //- p.some-info {{ props.value.info }}
            //- div.some-title 第 ({{ props.index + 1 }}) 张图片
            div.some-title {{ props.value.user}}
            div.img-info-to-left {{props.value.modeltype}}

          //- .img-group(slot-scope="props"){
            position: relative;
            display: inline-block
          //- }
          //- .img(slot="src")

        //- 自定义加载动画
        //- div(slot="loading" slot-scope="{isFirstLoad}")
          div(slot="loading" v-if="isFirstLoad") first-loading...
          div(v-else) loading...
</template>

<script>
import vueWaterfallEasy from 'vue-waterfall-easy'
import { Navbar } from '../../layout/components'
// import axios from "axios";
export default {
  name: 'App',
  components: {
    vueWaterfallEasy,
    Navbar
  },
  data() {
    return {
      imgsArr: [],
      group: 0, // 当前加载的加载图片的次数
      pullDownDistance: 0,
      searchKey: ''
    }
  },
  methods: {
    getData() {
      // axios.get('./static/mock/data.json?group=' + this.group) // 真实环境中，后端会根据参数group返回新的图片数组，这里我用一个静态json文件模拟
      //   .then(res => {
      //     this.group++
      //     if (this.group === 10) { // 模拟已经无新数据，显示 slot="waterfall-over"
      //       this.$refs.waterfall.waterfallOver()
      //       return
      //     }
      //     this.imgsArr = this.imgsArr.concat(res.data)
      //   })
      // if (this.group === 10) { // 模拟已经无新数据，显示 slot="waterfall-over"
      //   this.$refs.waterfall.waterfallOver()
      //   return
      // }

      const res = []
      for (var i = 0; i < 50; i++) {
        var num = Math.floor(Math.random() * 113) + 1
        var ext = 'png'
        var username = 'jason'
        var modeltypename = 'Lora'
        if (num > 35 && num < 51) {
          ext = 'jpg'
          username = 'yadong'
          modeltypename = 'checkpoint'
        }

        res.push({
          src: require('../../assets/images/jdb-ai-ad-' + num + '.' + ext),
          // href: 'https://www.baidu.com',
          info: '一些图片描述文字',
          user: username,
          modeltype: modeltypename
        })
      }
      this.imgsArr = this.imgsArr.concat(res)
    },

    clickFn(event, { index, value }) {
      // event.preventDefault()
      if (event.target.tagName.toLowerCase() === 'img') {
        console.log('image clicked', index, value)
      }
    },

    imgErrorFn(imgItem) {
      console.log('图片加载错误', imgItem)
    },

    // changeImgArr() {
    //   axios
    //     .get("./static/mock/data-change.json") // 真实环境中，后端会根据参数group返回新的图片数组，这里我用一个静态json文件模拟
    //     .then((res) => {
    //       this.imgsArr = res.data;
    //     });
    // },
    pullDownMove(pullDownDistance) {
      // console.log('pullDownDistance', pullDownDistance)
      this.pullDownDistance = pullDownDistance
    },

    pullDownEnd(pullDownDistance) {
      console.log('pullDownEnd')
      if (this.pullDownDistance > 50) {
        alert('下拉刷新')
      }
      this.pullDownDistance = 0
    }
  },
  created() {
    this.getData()

    // 删除某个卡片
    // setTimeout(()=>{
    //   this.imgsArr.splice(1,1)
    // },2000)
  }
}
</script>

<style lang="scss">
* {
  margin: 0;
  padding: 0;
}

a {
  color: #000;
  text-decoration: none;
  &:active {
    color: #000;
  }
}
html,
body,
#app {
  height: 100%;
}
.typetype button {
  cursor: pointer;
  font-size: 18px;
  padding: 0 10px;
}
#app {
  position: relative;
  #header {
    display: block;
    text-align: center;
    background: #000;
    color: #cccccc;
    line-height: 32px;
    font-size: 16px;
    font-weight: bold;
    letter-spacing: 2px;
    position: fixed;
    z-index: 999;
    width: 100%;
  }
  #content {
    position: absolute;
    top: 32px;
    bottom: 0;
    width: 100%;
  }
}
// .__err__ .img-wraper {
//   background: url(/static/img/1.jpg) no-repeat center/100px 100px !important;
// }
#app {
  overflow: auto;
  position: relative;

  .img-info-to-left {
    position: absolute; z-index:2; top: 10px; left: 10px; background:rgb(47, 45, 45); color: #fff; font-weight: bold;
  }

  // .some-info {
  //   line-height: 1.6;
  //   text-align: center;
  // }

  .some-info {
    position: absolute; z-index:2; bottom: 80px; right: 20px; background:rgb(22, 22, 22); color: #fff;
  }

  .some-title {
    position: absolute; z-index:2; bottom: 20px; left: 20px; opacity: 0.5; background:#000; color: #fff;
  }
}
</style>
