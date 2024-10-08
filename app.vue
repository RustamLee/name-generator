<script setup lang="ts">
import Name from "./components/Name.vue";
import { Gender, Popularity, Length, names } from "@/data";

interface OptionState {
  gender: Gender;
  popularity: Popularity;
  length: Length;
}

const options = reactive<OptionState>({
  gender: Gender.GIRL,
  length: Length.SHORT,
  popularity: Popularity.TRENDY,
});
const selectedNames = ref<string[]>([]);
const removeName = (index: number) => {
  const filteredNames = [...selectedNames.value];
  filteredNames.splice(index, 1);
  selectedNames.value = filteredNames;
};
const optionArray = [
  {
    title: "1. Choose a gender",
    category: "gender",
    buttons: [Gender.GIRL, Gender.UNISEX, Gender.BOY],
  },
  {
    title: "2. Choose the name's popularity",
    category: "popularity",
    buttons: [Popularity.TRENDY, Popularity.UNIQUE],
  },
  {
    title: "3. Choose name's length",
    category: "length",
    buttons: [Length.LONG, Length.ALL, Length.SHORT],
  },
];

const computeSelectedNames = () => {
  const filterNames = names
    .filter((name) => name.gender === options.gender)
    .filter((name) => name.popularity === options.popularity)
    .filter((name) => {
      if (options.length === Length.ALL) return true;
      else return name.length === options.length;
    });
  selectedNames.value = filterNames.map((name) => name.name);
};
</script>

<template>
  <div class="container">
    <h1>Baby Name Generator</h1>
    <p>Choose your options and click "Find Names" button</p>
    <div class="options-container">
      <Option
        v-for="option in optionArray"
        :key="option.title"
        :option="option"
        :options="options"
      >
      </Option>
      <button class="primary" @click="computeSelectedNames">Find Names</button>
    </div>
    <div class="cards-container">
      <Name
        v-for="(name, index) in selectedNames"
        :key="name"
        :name="name"
        @remove="() => removeName(index)"
        :index="index"
      >
      </Name>
    </div>
  </div>
</template>

<style scoped>
.cards-container {
  display: flex;
  margin-top: 3rem;
  flex-wrap: wrap;
}

.primary {
  background-color: rgb(249, 87, 89);
  color: white;
  border-radius: 6.5rem;
  border: none;
  padding: 0.75rem 4rem;
  font-size: 1rem;
  margin-top: 1rem;
  cursor: pointer;
}

.container {
  margin: 0 auto;
  font-family: Arial, Helvetica, sans-serif;
  color: rgb(27, 60, 138);
  max-width: 50rem;
  text-align: center;
}
h1 {
  font-size: 3rem;
}
.options-container {
  background-color: rgb(255, 238, 236);
  border-radius: 2rem;
  padding: 1rem;
  width: 95%;
  margin: 0 auto;
  margin-top: 4rem;
  position: relative;
}
</style>
