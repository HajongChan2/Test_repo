<template>
    <div class="con">
        <div class="container">
            <h2>HelloWorld</h2>
            <div class="personal">
                <input type="text" v-model="value" @input="value = value.replace(/[^0-9]/g, '')" maxlength="5" id="personal_number" placeholder="고번입력란 (숫자만 입력)">
                <label for="personal_number" id="personal_num"></label>
            </div>
            <div class="select">
                <select name="select" id="select">
                    <option value="one">범죄압류</option>
                    <option value="two">일반압류</option>
                    <option value="three">보호구역 압류</option>
                    <option value="four">원격폐차</option>
                </select>
            </div>
            <button @click="test" id="btn">출력</button>
        </div>
    </div>
    
</template>
<script>

export default {
    name: 'TestText',
    data(){
        return{
            value : ''
        }
    },
    methods:{
        test(){
            let num = document.getElementById('personal_number').value;
            let select = document.getElementById('select').value;
            this.$emit('send-data', {
                num,
                select
            })
        }
    }
}


</script>
<style>
.con{
    display: flex;
    flex-direction: column;
    align-items: center;
}
.container{
    width: 350px;
    text-align: center;
}
.container > *{
    margin: 20px 0;
}
.personal{
    position: relative;
    overflow: hidden;
}
#personal_number{
    width: 100%;
    height: 40px;
    padding-left: 25px;
    font-size: 13px;
    letter-spacing: .15px;
    border: none;
    outline: none;
    font-family: 'Montserrat', sans-serif;
    background-color: #ecf0f3;
    transition: .25s ease;
    border-radius: 8px;
    box-shadow:
      inset 2px 2px 4px #d1d9e6,
      inset -2px -2px 4px #f9f9f9;
}
#personal_number:focus{
    box-shadow:
        inset 4px 4px 4px #d1d9e6,
        inset -4px -4px 4px #f9f9f9;
}
#select{
    width: 100%;
    height: 40px;
    padding-left: 25px;
    -webkit-appearance: none;  /* 크롬 화살표 없애기 */
    -moz-appearance: none; /* 파이어폭스 화살표 없애기 */
    appearance: none;  /* 화살표 없애기 */
    border-color: #d1d9e6;
    border-radius: 8px;
    background-color: #ecf0f3;
}

#btn{
    margin:10px 0;
    width: 100%;
    height: 40px;
    border-color: #d1d9e6;
    border-radius: 8px;
    background-color: #ecf0f3;
    box-shadow: none;
}

</style>