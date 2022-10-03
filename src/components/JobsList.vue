<template>
  <div class="job-list">
    <p>Ordered by {{ order }}</p>
    <ul>
      <li v-for="job in orderJobs" :key="job.id">
        <h2>{{ job.title }} in {{ job.location }}</h2>
        <div class="salary">
          <p>{{ job.salary }} rupees</p>
        </div>
        <div class="description">
          Lorem, ipsum dolor sit amet consectetur adipisicing elit. Incidunt
          numquam minus debitis aliquid, a quisquam, aliquam non necessitatibus
          tempore dolorum cum! Eos quia ex, soluta culpa dicta beatae ab vel!
        </div>
      </li>
    </ul>
  </div>
</template>
<script lang="ts">
import { computed, defineComponent, PropType } from "vue";
import Job from "@/types/Jobs";
import OrderTerm from "@/types/OrderTerm";
import { propsToAttrMap } from "@vue/shared";

export default defineComponent({
  props: {
    jobs: {
      required: true,
      type: Array as PropType<Job[]>,
    },
    order: {
      required: true,
      type: String as PropType<OrderTerm>,
    },
  },
  setup(props) {
    const orderJobs = computed(() => {
      return [...props.jobs].sort((a: Job, b: Job) => {
        return a[props.order] > b[props.order] ? 1 : -1;
      });
    });
    return { orderJobs };
  },
});
</script>

<style scoped>
.job-list {
  max-width: 960px;
  margin: 40px auto;
}
.job-list li {
  list-style-type: none;
  background: white;
  padding: 16px;
  margin: 16px 0;
  border-radius: 4px;
}
.job-list h2 {
  margin: 0 0 10px;
  text-transform: capitalize;
}
.salary {
  display: flex;
}
.salary p {
  color: #17bf66;
  font-weight: bold;
  margin: 10px 4px;
}
</style>
