<template>
    <button @click='onClick()' :style='{ background: color }'>
        {{ text }}
    </button>
</template>

<script>
export default {
  name: 'Button',
  props: {
    color: String,
    text: String,
  },
  methods: {
    onClick() {
      this.$emit('btn-click');
    },
  },

};
</script>

<style scoped>
button {
  padding: 2vw;
  color: white;
  font-family: Poppins;
  border: none;
  border-radius: 5px;
  cursor: pointer;
  transition: background-color 0.5s ease;
}
button:hover {
  background-color: rgb(255, 208, 0) !important;
}
button:active {
  background-color: rgb(0, 255, 170) !important;
}
</style>
