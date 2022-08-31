<template>
  <div class="input-wrapper">
    <label>{{label}}</label>
    <div style="display: flex;flex-direction: column">
      <input
          type="text"
          :value="value"
          class="input-style"
          :name="name"
          :placeholder="showPlaceholderText"
          :style="{width:`${width}px`,height:`${height}px`}"
          @input="onInput"
          @change="onChange"
      />
      <span v-if="error" class="error-style">{{error}}</span>
    </div>
  </div>
</template>

<script>
export default {
  name: "InputCustom",
  props: {
    value: { //enter 누를때 바인딩asa
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
      error:'',
    }
  },
  computed: {
    name() {
      return this.label.toLowerCase();
    },
    showPlaceholderText(){
      return !this.value ? this.placeholder : ''
    },

  },
  methods: {
    onInput(e){
      const value=e.target.value;
      if (!value) {
        this.error = 'Value should not be empty';
      }else{
        this.error = ''
      }
      this.$emit('input',value)
    },
    onChange(e){
      this.$emit('change',e.target.value)
    }
  },
}
</script>

<style scoped>
.input-wrapper{
  display: flex;
}
.input-style{
  border-radius: 5px;
  font-size: 13px;
  border : 2px solid rgba(0,0,0,.87);
  color: #000000;
}
.error-style{
  font-size: 8px;
  padding-left: 8px;
  color : #ff5252 !important;
}

</style>