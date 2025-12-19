<template>
  <Test @send-data="receiveData" />
  <div class="text_box">
    <div class="text" @click="handleCopy">{{ message }}</div>
    <div v-if="showCount">{{ count }}초</div>
  </div>
</template>

<script>
import Test from './components/Test.vue'
import messageData from './assets/test.json'

export default {
  name: 'App',
  components: {
    Test
  },
  methods: {
    receiveData(payload) {
      this.num = payload.num;
      this.select = payload.select;
      this.message = messageData[0][this.select].replace('{num}', this.num);
      this.handleCopy()
    },
    handleCopy() {
      // 기존 타이머 있으면 제거
      if (this.timer) {
        clearInterval(this.timer)
        this.timer = null
        this.count = 60
      }

      if (this.select === 'two') {
        this.showCount = true
        this.copyText();
        this.timer = setInterval(() => {
          this.count--
          if (this.count === 0) {
            clearInterval(this.timer)
            this.timer = null
            this.showCount = false;
            this.count = 60
            console.log(this.showCount)
          }
        }, 1000)

      } else {
        this.copyText()
        this.showCount = false;
      }
    },
    copyText() {
      navigator.clipboard.writeText(this.message)
        .then(() => {
          console.log('복사 완료')
        })
        .catch(err => {
          console.error('복사 실패', err)
        })
    }
  },
  data(){
        return{
            num : '',
            select : '',
            message: '',
            count : 60,
            showCount : false,
            timer: null
        }
  },
}

</script>

<style>
#app {
  margin:0 auto;
  box-sizing: border-box;
  padding:0;
  
}
.text_box{
  display: flex;
  margin: 30px 0;
  flex-direction: column;
  align-items: center;
}    
.text{
  width: 50%;
  height: 150px;
  border: solid 1px #d9d9d9;
  border-radius: 8px;
  padding:10px;
  cursor: pointer;
}
</style>
