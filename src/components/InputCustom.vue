<template>
  <div>
    <label>
      {{label}}
      <input
          type="text"
          :name="name"
          v-model="innerValue"
          :placeholder="showPlaceholderText"
          @change="onChange"
          @focus="onFocus"
          @blur="onBlur"
          :style="{width:`${width}px`,height:`${height}px`}"
          :class="{'click-border':isFocus}"
          class="input-style"
      />
    </label>
  </div>
</template>

<script>
export default {
  name: "InputCustom",
  emits:["change","on-focus"],
  props: {
    value: { //input 이벤트로 적은값
      type: [Number,String],
    },
    label:{
      type:String,
      default:undefined
    },
    placeholder: {
      type: String,
      default: undefined
    },
    width:{
      type:String,
      default:''
    },
    height:{
      type:String,
      default:''
    }

  },
  data() {
    return {
      innerValue: '',//input 값
      isFocus: false //input을 클릭했는지 여부

    }
  },
  computed: {
    name() {
      return this.label.toLowerCase();
    },
    showPlaceholderText(){
      return !this.isFocus ? this.placeholder : ''
    }
  },
  methods: {
    /**
     * input을 클릭할때
     */
    onFocus() {//TODO::input을 클릭했을때 스타일 먹이고 다른쪽 클릭할때 스타일이 없어져야됨
      this.isClick = true
    },
    onBlur(){
      this.isClick = false
    },
    /**
     * input 값을 입력했을때
     */
    onChange() {
      if(this.innerValue === this.value) return
      this.$emit("input",this.innerValue)
      this.innerValue =undefined

    }

  },
}
</script>

<style scoped>
.init-style{
  border: 0;
}
.click-border{
  border:2px solid red !important;
}
.input-style{
  border-radius: 5px;
  font-size: 13px;
  color: #808080;
}
</style>