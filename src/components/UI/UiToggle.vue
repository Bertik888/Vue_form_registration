<template>
  <div class="ui-toggle">
    <input 
      class="ui-toggle__input" 
      type="checkbox" 
      role="switch" 
      :value="modelValue"
      :checked="modelValue"
      @change="$emit('update:modelValue', $event.target.checked)"
    >
  </div>
</template>

<script>
export default {
  name: 'UiToggle',
  props: {
    modelValue: {
      type: String,
      default: ''
    }
  }
}
</script>

<style lang="scss" scoped>
@import '@/assets/css/variables.scss';

.ui-toggle { 

  &__input {
    width: 39px;
    height: 19px;
    background-position: left center;
    border-radius: 19px;
    transition: background-position .15s ease-in-out;
    vertical-align: top;
    background-color: #fff;
    background-repeat: no-repeat;
    background-position: center;
    background-size: contain;
    border: 1px solid rgba(0,0,0,.25);
    -webkit-appearance: none;
    -moz-appearance: none;
    appearance: none;
    -webkit-print-color-adjust: exact;
    color-adjust: exact;
    background-image: url("data:image/svg+xml,%3csvg xmlns='http://www.w3.org/2000/svg' viewBox='-4 -4 8 8'%3e%3ccircle r='3' fill='rgba%280, 0, 0, 0.25%29'/%3e%3c/svg%3e");
    background-position: left center;
    cursor: pointer;
    
    &:checked {
      background-position: right center;
      background-image: url("data:image/svg+xml,%3csvg xmlns='http://www.w3.org/2000/svg' viewBox='-4 -4 8 8'%3e%3ccircle r='3' fill='%23fff'/%3e%3c/svg%3e");
      background-color: $blue-1;
      border-color: $blue-1;
    }
  }
}
</style>
