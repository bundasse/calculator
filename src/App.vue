<template>
  <div class="h-full min-h-screen bg-orange-100 p-3 md:p-10">
    <div class="max-w-4xl mx-auto border rounded-md bg-white pb-10 border-orange-200">
      <div class="my-10">
        <div class="imgTitle">
          <img src="./assets/pie.png" alt="logo" class="w-40 block mx-auto mb-5">
        </div>
        <div class="text-center">
          <h1 class="text-6xl font-extrabold mb-6 text-amber-500">비<span class="text-rose-600">율</span> 계<span class="text-rose-600">산</span>기</h1>
          <p class="px-5">입력칸에는 숫자만 입력해주세요. %등은 입력하지 않아도 괜찮습니다.</p>
          <div class="flex justify-center gap-5 md:gap-10 mt-2">
            <div class="w-32 md:w-40 border border-gray-300">
              <span class="text-sm">소수점 자리</span>
              <select v-model="sosu" class="text-sm w-12 text-center">
                <option v-for="e in 5" :key="e" :value="e-1">{{ e-1 }}</option>
              </select>
            </div>
              <button class="w-40 bg-rose-500 text-white font-bold p-1 rounded-md" @click="reset()">모든 값 리셋!</button>
          </div>
        </div>
      </div>
      <div class="px-4 md:px-10 py-5 mb-3 flex flex-wrap">
        <h3 class="title">퍼센트 비율 값 계산</h3>
        <div class="w-full lg:w-3/5 mb-3">
          <input type="text" @input="bindNumber" @change="UpdateCalc" v-model="calc1" class="inputBox" placeholder="전체값 100"> <span class="mr-2">의</span>
          <input type="text" @change="UpdateCalc" v-model="calc2" class="inputBox" placeholder="비율값 20"> <span class="mr-2">%는</span>
        </div>
        <div class="w-full lg:w-2/5 mb-3">
          <input type="text" :value="ResultCalcA" readonly class="inputBox" placeholder="일부값 20"> <span>입니다.</span>
        </div>
      </div>
      <div class="px-4 md:px-10 py-5 mb-3 flex flex-wrap">
        <h3 class="title">일정 값 비율 계산</h3>
        <div class="w-full lg:w-3/5 mb-3">
          <input type="text" v-model="calc3" class="inputBox" placeholder="전체값 100"> <span class="mr-2">의</span>
          <input type="text" v-model="calc4" class="inputBox" placeholder="일부값 20"> <span class="mr-2">은(는)</span>
        </div>
        <div class="w-full lg:w-2/5 mb-3">
          <input type="text" :value="ResultCalcB" readonly class="inputBox" placeholder="비율값 20"> <span>%입니다.</span>
        </div>
      </div>
      <div class="px-4 md:px-10 py-5 mb-3 flex flex-wrap">
        <h3 class="title">변경값 비율 계산</h3>
        <div class="w-full lg:w-3/5 mb-3">
          <input type="text" v-model="calc5" class="inputBox" placeholder="기준값 100"> <span class="mr-2">이(가)</span>
          <input type="text" v-model="calc6" class="inputBox" placeholder="변경값 20"> <span class="mr-2">로 변경되면</span>
        </div>
        <div class="w-full lg:w-2/5 mb-3">
          <input type="text" :value="ResultCalcC" readonly class="inputBox" placeholder="80% 감소"> <span>입니다.</span>
        </div>
      </div>
      <div class="px-4 md:px-10 py-5 mb-3 flex flex-wrap items-start">
        <h3 class="title">기존 > 변경값 비율 계산</h3>
        <div class="w-full lg:w-[60%] mb-5">
          <input type="text" v-model="calc7" class="inputBox" placeholder="기준값 100"> <span class="mr-2">값이</span>
          <input type="text" v-model="calc8" class="inputBox" placeholder="비율값 20"> <span class="mr-2">% 변경될 시</span>
        </div>
        <div class="w-full lg:w-[40%] flex flex-col pl-10 lg:pl-0">
          <div class="mb-3">
            <span class="mr-2">증가값 : </span>
            <input type="text" :value="ResultCalcD" readonly class="inputBox" placeholder="120"> <span>입니다.</span>
          </div>
          <div>
            <span class="mr-2">감소값 : </span>
            <input type="text" :value="ResultCalcE" readonly class="inputBox" placeholder="80"> <span>입니다.</span>
          </div>
        </div>
      </div>
      <div class="px-4 md:px-10 py-5 mb-3 flex flex-wrap items-start">
        <h3 class="title">비율 고정 계산</h3>
        <div class="w-full lg:w-1/2 mb-5">
          <input type="text" v-model="calc9" class="inputBox" placeholder="기준값1 100"> <span class="mr-2">:</span>
          <input type="text" v-model="calc10" class="inputBox" placeholder="기준값2 20"> <span class="mx-2"> =</span>
        </div>
        <div class="w-full lg:w-1/2 mb-5">
          <input type="text" v-model="calc11" class="inputBox" placeholder="기준값3 50"> <span class="mr-2">:</span>
          <input type="text" :value="ResultCalcF" readonly class="inputBox" placeholder="10">

        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'App',
  data() {
    return {
      calc1:'',
      calc2:'',
      calc3:'',
      calc4:'',
      calc5:'',
      calc6:'',
      calc7:'',
      calc8:'',
      calc9:'',
      calc10:'',
      calc11:'',
      sosu:'2'
    }
  },
  methods: {
    reset(){
      for(let i = 0; i < document.querySelectorAll('.inputBox').length; i++){
        document.querySelectorAll('.inputBox')[i].value = '';
      }
    },
    bindNumber(e){
      this.calc1 = e.target.value;
    }
  },
  computed:{
    ResultCalcA(){
      return this.calc1 === '' || this.calc2 === '' ? '': (Number(this.calc1)*Number((this.calc2)/100)).toFixed(this.sosu) ;
// v-model은 숫자건 뭐건 문자열로 취급하는 습성이 있다...
    },
    ResultCalcB(){
      return this.calc3 === '' || this.calc4 === '' ? '': ((100*Number(this.calc4))/Number(this.calc3)).toFixed(this.sosu);
    },
    ResultCalcC(){
      let a = (Number(this.calc6)-Number(this.calc5))/Number(this.calc5)*100;
      return this.calc5 === '' || this.calc6 === '' ? '': a >0 ? a.toFixed(0)+'% 증가' : (a*(-1)).toFixed(0)+'% 감소' 
    },
    ResultCalcD(){
      let d = Number(this.calc7)+(Number(this.calc7)*Number(this.calc8)/100);
      return this.calc7 === '' || this.calc8 === '' ? '': d.toFixed(this.sosu); 
    },
    ResultCalcE(){
      let e = Number(this.calc7)-(Number(this.calc7)*Number(this.calc8)/100);
      return this.calc7 === '' || this.calc8 === '' ? '': e.toFixed(this.sosu); 
    },
    ResultCalcF(){
      let f = (Number(this.calc10)*Number(this.calc11))/Number(this.calc9);
      if(this.calc9 === '' || this.calc10 === '' || this.calc11 === ''){
        return '';
      }else{
        return f.toFixed(this.sosu); 
      }
    }
  },
  watch:{
    calc1 : function() {
      return this.calc1 = this.calc1.replace(/[^0-9]/g, '')      
    },
    calc2 : function() {
      return this.calc2 = this.calc2.replace(/[^0-9]/g, '')      
    }
  }, // watch는 요소 자체를 바로 감시하는 역할이다!
  components: {
  }
}
</script>

<style>
.imgTitle{
  background: url('./assets/bg_pie.png') repeat-x center center;
}
</style>
