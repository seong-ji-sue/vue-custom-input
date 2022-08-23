<template>
  <div>
    <label style="display: flex">
      <span>{{label}}</span>
      <div style="display: flex;flex-direction: column">
        <input
            type="text"
            :name="name"
            v-model="model"
            :placeholder="showPlaceholderText"
            @focus="onFocus"
            @blur="onBlur"
            :style="{width:`${width}px`,height:`${height}px`}"
            :class="{'click-border':isClick}"
            class="input-style"
        />
        <span v-if="error" class="error-style">{{error}}</span>
      </div>
    </label>

  </div>
</template>

<script>
export default {
  name: "InputCustom",
  emits:["change","on-focus"],
  props: {
    value: { //enter 누를때 바인딩
      type: String,
      required: true,
    },
    label:{
      type:String,
      default:undefined,
      required: true,
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
      isClick:false,
      error:''
    }
  },
  computed: {
    name() {
      return this.label.toLowerCase();
    },
    showPlaceholderText(){
      return !this.value ? this.placeholder : ''
    },
    model:{
      get(){
        return this.value;
      },
      set(value){
        if (!value) {
          this.error = 'Value should not be empty';
        }else{
          this.error = ''
        }
        this.$emit('input',value)
      }
    }
  },
  methods: {
    /**
     * input을 클릭할때
     */
    onFocus() {
      this.isClick = true
    },
    onBlur(){
      this.isClick = false
    },

  },
}
</script>

<style scoped>
.click-border{
  border:1px solid red !important;
}
.input-style{
  border-radius: 5px;
  font-size: 13px;
  color: #000000;
}
.error-style{
  font-size: 8px;
  color: palevioletred;
}

</style>