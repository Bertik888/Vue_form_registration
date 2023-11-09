<template>
  <div class="wrapper">
    <form-block />
  </div>
</template>

<script>
import FormBlock from '@/components/FormBlock.vue'

export default {
  name: 'App',
  components: {
    FormBlock    
  }
}
</script>

<style lang="scss">
.wrapper {
  background-color: #696977;
  display: flex;
  align-items: center;
  justify-content: center;
  position: fixed;
  top: 0;
  bottom: 0;
  left: 0;
  right: 0;
  padding: 30px;
}
</style>
