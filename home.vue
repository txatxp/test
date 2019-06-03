<template>
  <div class="home">
    <p class="name" @click="tos">名字name: {{getName}}</p>
    <button @click="setlt">设置lt</button>
    <br><br>
    <button @click="settxp">设置txp</button>
    <br><br>
    <input type="text" v-model="name">
    <button @click="setname">设置名字</button>
  </div>
</template>

<script>
// @ is an alias to /src
import HelloWorld from '@/components/HelloWorld.vue'
import { testAjax } from '@/http/tora-http/index'
export default {
  name: 'home',
  components: {
    HelloWorld
  },
  data () {
    return {
      name: ''
    }
  },
  async created () {

    Array.prototype.getDifferentArrayLength = function () {
      let arrlen = []
      let yArr = this
      var getArray = function (value) {
        let len = 0
        let arr = []
        yArr.forEach(function (item, index) {
          if (item.matnr == value) {
            arr.push(item)
          }
        })
        len = arr.length
        return len
      }
      yArr.forEach(function (item, index) {
        var len = getArray(item.matnr)
        if (len <= 1) {
          arrlen.push(item)
        }
      })
      return 	arrlen.length;
      
    }


    api.carrierNumberAjax(data).then(r => {
      if (r.body.statusCode === 3000) {
        this.SHOW_TOAST_LARGE({show: true, content: r.data})
      } else {
        if (r.body.result) {
          let data = r.body
          if (data.data.length) {
            this.tableList = data.data
            let len = this.tableList.getDifferentArrayLength()
            console.log(len, '这就是你要的不同数字的元素的个数')
          }
        }
      }
    })



    
    console.log(this.$store.getters['taroShareActivity/getName'])
    let type = 'slide'
    let testData = await testAjax({
      type
    })
    console.log(testData, 'testDatatestDatatestData')
  },
  computed: {
    getName () {
      return this.$store.getters['taroShareActivity/getName']
    }
  },
  methods: {
    tos () {
    },
    setlt () {
      this.$store.dispatch('taroShareActivity/setLt')
    },
    settxp () {
      this.$store.dispatch('taroShareActivity/setTxp')
    },
    async setname () {
      let name = this.name
      this.$store.dispatch('taroShareActivity/setName', {
        name
      })
    }
  }
}
</script>
<style lang="scss" scoped>
.name{
  font-size: 32px;
}
</style>
