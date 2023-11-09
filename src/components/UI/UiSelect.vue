<template>
  <div 
    class="ui-select" 
    :class="{ '_open': open }"
    @blur="open = false"
  >
    <div 
      class="ui-select__wrapper" 
      :class="{ '_invalid': invalidText }" 
      @click="open = !open"
    >
      <div class="ui-select__value">        
        {{ selected }}
      </div>
      <svg 
        xmlns="http://www.w3.org/2000/svg" 
        width="9" 
        height="5" 
        viewBox="0 0 9 5" 
        fill="none"
        class="ui-select__icon"
      >
        <path d="M8 1L4.5 4L1 1" stroke="#A7A7B6" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round"/>
      </svg>
    </div>
    <div 
      v-if="invalidText"
      class="ui-select__error"
    >
      {{ invalidText }}
    </div>
    <div class="ui-select__items">
      <div
        v-for="item in options"
        :key="item.value"
        @click="onSelected(item.value)"
      >
        {{ item.name }}
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    options: {
      type: Array,
      default: []
    },
    modelValue: {
      type: [String, Number],
      default: null
    },
    invalidText: {
      type: String,
      default: ''
    },
    label: {
      type: String,
      default: ''
    }
  },
  data() {
    return {
      open: false
    }
  },
  computed: {
    selected() {
      return this.options.find(item => item.value === this.modelValue)?.name || this.label
    }
  },
  methods: {
    onSelected(value) {
      this.open = false
      this.$emit('update:modelValue', value)
    }
  }
}
</script>

<style lang="scss" scoped>
@import '@/assets/css/variables.scss';

.ui-select {
  position: relative;  

  &__wrapper {
    border-radius: 11px;
    padding: 10px;
    border: 1px solid $grey-2;
    display: flex;
    align-items: center;
    cursor: pointer;
    line-height: 1;
    font-size: 14px;
    font-weight: 400;
    letter-spacing: -0.021px;
    color: $grey;
    width: 100%;

    &._invalid {
      border-color: red;
    }        
  }
  &._open {
    .ui-select__icon {
      transform: rotate(180deg);
    }
    .ui-select__items {
      display: block;
    }
  }

  &__value {
    width: 100%;
    height: 16px;
    display: flex;
    align-items: center;
  }

  &__icon {
    margin-left: 10px;
  }

  &__items {
    display: none;
    position: absolute;
    left: 0;
    right: 0;
    margin-top: 2px;
    z-index: 1;
    border-radius: 11px;
    overflow: hidden;
    border: 1px solid $grey-2;   
    background-color: white; 

    div {
      color: $grey-1;
      padding: 10px;
      cursor: pointer;
      transition: background-color .2s ease-in;

      &:hover {
        background-color: $grey-2; 
      }
    }
  }
  &__error {
    font-size: 12px;
    line-height: 1;
    color: red;
    position: absolute;
    bottom: -16px;
  }
}
</style>
