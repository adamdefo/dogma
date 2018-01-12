<template>
  <div class="orders">
    <h1>{{ title }}</h1>
  </div>
</template>

<script>
export default {
  name: 'Orders',
  data () {
    return {
      title: 'Orders'
    }
  }
}
</script>

<style lang="scss" scoped>
.orders {
  & h1 {
    color: red
  }
}
</style>
