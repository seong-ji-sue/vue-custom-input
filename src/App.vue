<template>
  <div>
    <div>value : {{inputValue}}</div>
    <input-custom
        v-model="inputValue"
        label="input custom"
        placeholder="여기에 입력하세요"
        width="150"
        height="25"

    ></input-custom>
  </div>
</template>

<script>

import InputCustom from "@/components/InputCustom";
export default {
  name: 'App',
  components: {
    InputCustom
  },
  data() {
    return {
      inputValue: '',
    }
  },
}
</script>

<style>
</style>
