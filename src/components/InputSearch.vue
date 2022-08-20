<template>
<div :class="[{gap: step===1},'search-container']">
  <input 
    type="text"
    :value="modelValue"
    @input="$emit('update:modelValue', $event.target.value)"
    :class="{dark}"
  >
  </div>
</template>


<script>


export default {
  
  name: 'InputSearch',
  props: {
    modelValue: String,
    dark: {
      type: Boolean,
      default: false
    }
  }
}
</script>

<style lang="less" scoped>

@color-light: #fff;
@color-dark: #222;

.search-container {
  text-align: center;
  padding-top: 60px;

  &.gap {
    padding-top: 180px;
    margin-bottom: 60px;
  }
}

input {
  background: none;
  outline: none;
  text-align: center;
  font-size: 16px;
  font-weight: bold;
  text-transform: uppercase;
  letter-spacing: 3px;
  border: none;
  border-bottom: 1px solid @color-light;
  color: @color-light;
  margin: 0 auto;
  padding: 8px 0;
  transition: all .2s linear;

  &:hover,
  &:focus {
    box-shadow: 0px 14px 15px -13px @color-light
  }

  &.dark {
    border-bottom: 1px solid @color-dark;
    color: @color-dark;

    &:hover,
    &:focus {
        box-shadow: 0px 14px 15px -13px @color-dark
    }
  }
}

</style>
