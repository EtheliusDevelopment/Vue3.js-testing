<template>
  <header>
    <h1>{{ title }}</h1>
    <Button @btn-click="$emit('toogle-add-task')"  :text="showAddTask ? 'Close' : 'Add Task' " 
    :color="showAddTask ? 'red' : 'green' "/>
    </header>
</template>

<script>
import Button from './Button.vue';

export default {
  name: 'Headerr',
  props: {
    title: {
      default: 'TITOLODEFAULT',
    },
    showAddTask: Boolean,
  },
  components: {
    Button,
  },
};
</script>

<style scoped>
header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 20px;
}
</style>
