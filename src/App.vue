<template>
  <div class="app">
    <header>
      <button @click="handleClick('title')">order by title</button>
      <button @click="handleClick('salary')">order by salary</button>
      <button @click="handleClick('location')">order by location</button>
    </header>
    <jobs-list :jobs="jobs" :order="order" />
  </div>
</template>

<script lang="ts">
import { defineComponent, reactive, ref, toRefs } from "vue";
import Job from "./types/Jobs";
import JobsList from "./components/JobsList.vue";
import OrderTerm from "./types/OrderTerm";

export default defineComponent({
  name: "App",
  components: { JobsList },
  setup() {
    // const state = reactive({
    //   name: "Link",
    //   age: 25 as string | number,
    // });
    // state.name = 99 // cannont change the type
    // state.age = '26'
    // return { ...toRefs(state) };
    // const name = ref("Link");
    // const age = ref<number | string>(25);
    // return { name, age };
    const jobs = ref<Job[]>([
      {
        title: "farm worker",
        location: "lon lon ranch",
        salary: 30000,
        id: "1",
      },
      {
        title: "quarryman",
        location: "death mountain",
        salary: 40000,
        id: "2",
      },
      {
        title: "flute player",
        location: "the lost woods",
        salary: 35000,
        id: "3",
      },
      {
        title: "fisherman",
        location: "lake hylia",
        salary: 21000,
        id: "4",
      },
    ]);

    const order = ref<OrderTerm>("title");

    const handleClick = (term: OrderTerm) => {
      order.value = term;
    };
    return { jobs, handleClick, order };
  },
});
</script>

<style> </style>
