<template>
  <div class="card-container">

  </div>
</template>

<script>

export default {
  name: 'Card',
  props: {
    msg: String,
    isFlipped: Boolean,
    id: Number,
  },
  setup(props) {

    return {props}
  },
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.hello {
  font-size: 10vh;;
}
</style>
