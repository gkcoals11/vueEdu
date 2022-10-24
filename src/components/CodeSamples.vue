<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <div class="area">
      <!-- mustache -->
        <div class="next">
          <h1 class="highlight"> 머스태치 </h1>
          <div> {{ mustache }} </div>
          <div>{{ syntaxes[0] }}</div> <!-- 배열 바인딩 가능 -->
          <div>{{ 113 + 113 }}</div> <!-- 내부에서 연산이 가능하다 -->
          <div>{{ '문자열' }}</div>
        </div>
        <!-- v-bind -->
        <div class="next">
          <h1 class="highlight"> v-bind 단방향 바인딩 </h1>
          <h4 class="text_red">클래스 사용</h4>
          <h4 v-bind:class="color_green"> 동적 스타일 바인딩 사용</h4> <!-- v-bind를 사용해서 변수 color_red의 'text_red'를 동적 바인딩-->
          <h4 :class="{'text_green' : returnTrue()}">객체 바인딩</h4>
          <h4 :class="['text_green', 'highlight']">배열 바인딩</h4> <!-- 스타일 바인딩 오른쪽 조건이 true일 때 왼쪽의 클래스를 바인딩한다 -->
          <input :value="vBind" class="ipt-tag"/>
        </div>``
        <!-- v-model -->
        <div class="next">
          <h1 class="highlight"> v-model 양방향 바인딩 </h1>
          <input type="text" class="ipt-tag" v-model="vModel"/>
          <div>
            <label>체크박스</label>
          <input type="checkbox" v-model="vModel_check"/>
          </div>
        </div>
        <!-- v-show -->
        <h1>조건부 렌더링</h1>
        <div class="next">
          <h1 class="highlight"> v-show </h1>
          <div v-show="vShow" class="box"/>
          <button v-on:click="vShowToggle" >v-show</button>
          <!-- v-on 디렉티브(이벤트핸들러) -->
          <!-- onClick="vShowToggle()"  -->
        </div>
        <!-- v-if -->
        <div class="next">
          <h1 class="highlight"> v-if </h1>
          <div v-if="vIf" class="box"/>
          <button @click="vIfToggle">v-if</button>
        </div>
        <div class="next">
          <h1 class="highlight"> v-for </h1>
          <ol>
            <h4>index, item 배열 바인딩</h4>
            <div v-for="(item, index) in vFors1" :key="index">
            {{  'index: ' + index + ' | ' + 'data:' + item }}
            <br/>
            </div>
            <br/>
            <h4> 내부의 key, value를 이용한 object가 들어간 배열 바인딩</h4>
            <div v-for="item in vFors2" :key="item.key">
            {{  'index: ' + item.key + ' | ' + 'data:' + item.value }}
            <br/>
            </div>
          </ol>
        </div>
        <div class="next">
          <h1 class="highlight"> computed </h1>
          <input type="text" v-model="vModel_computed"/>
          <p>{{ reversedMessage }}</p>
          <p>{{ vModel_watch }}</p>
          
          <!-- <a> {{ this.reversedMessage()}} </a> -->
        </div>
      </div>
  </div>
</template>

<script>

export default {
  name: 'CodeSamples',
  props: {
    msg: String // App(parent)에서 상속받은 props
  },
  data () {
    return {
      // mustache
      mustache: '문자열 바인딩',
      syntaxes: ['Mustache syntax'],
      // v-bind
      vBind: 'v-Bind 단방향 데이터 바인딩',
      color_green: 'text_green', // 데이터에 css 클래스 바인딩
      // v-model
      vModel: 'v-model입니다.',
      vModel_check: false,
      // v-show
      vShow: true,
      // v-if
      vIf: true,
      // v-for
      vFors1: ['데이터1', '데이터2', '데이터3', '데이터4', '데이터5'],
      vFors2: [ {key: 'data1', value: '데이터1'}, {key: 'data2', value: '데이터2'}, {key: 'data3', value: '데이터3'}, {key: 'data4', value: '데이터4'}],
      // computed
      vModel_computed: 'text',
      // watch
      vModel_watch: ''      
    }
  },
  beforeCreate () {console.log('beforeCreate')},
  created () {console.log('created')},
  beforeMount () {console.log('beforeMount')},
  mounted () {console.log('mounted')},
  beforeUpdate () {console.log('beforeUpdate')},
  updated () {console.log('updated')},
  beforeUnmount () {console.log('beforeUnmount')},
  unmounted () {console.log('unmounted')},
  beforeDestroy () { console.log('beforeDestroy')},
  computed: { // 반응형 getter ex)store getter를 사용해서 반응성 부여
    reversedMessage () {
      return this.vModel_computed.split('').reverse().join('')
    }
  },

watch: { // 대상 데이터의 변경을 감시하고 콜백함수를 실행
  vModel_computed: function (newVal, oldVal) {
    console.log(oldVal)
    this.vModel_watch = newVal.split('').reverse().join('')
  }
},

methods: {
    returnTrue () { // true를 반환하는 함수
      return true
    },
    vShowToggle () { // v-show
      console.log('vShow')
      this.vShow === true ? this.vShow = false : this.vShow = true
    },
    vIfToggle () { // v-if
      console.log('vIf')
      this.vIf === true ? this.vIf = false : this.vIf = true
    }
  }
}
</script>



<style scoped>
.area {
  border: 1px solid black;
  margin: 5px
}
.next {
  border-bottom: 1px solid black;
}
.highlight {
  font-weight: bolder;
}
.text_green {
  color: rgb(112, 185, 122);
}
.ipt-tag {
  width: 200px;
}
.box {
  width: 100px;
  height: 100px;
  position: relative;
  left: 45%;
  /* top: 50%;
  transform: translate(-50%, -50%); */
  border: 1px solid black;
  margin: 20px
  
}
</style>
