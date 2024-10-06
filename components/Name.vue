<script setup lang="ts">
const props = defineProps<{
  name?: string;
  index?: number;
}>();
const emit = defineEmits(["remove"]);
const removeName = () => {
  emit("remove", props.index);
};
</script>
<template>
  <div class="card">
    <h4>{{ name }}</h4>
    <p @click="removeName">x</p>
  </div>
</template>

<style scoped>
.card {
  background-color: rgb(27, 60, 138);
  width: 28%;
  color: white;
  border-radius: 1rem;
  padding: 0.5rem;
  margin-right: 0.5rem;
  margin-bottom: 1rem;
  position: relative;
}
.card p {
  position: absolute;
  top: -20%;
  left: 92.5%;
  color: rgb(255, 255, 255 0.178);
  cursor: pointer;
}
</style>
