<template>
  <NavBar @search="handleSearch"></NavBar>
  <div class="job-offers-container">
    <JobOffer
      v-for="job in shownJobOffers"
      :key="job.id"
      :title="job.title"
      :description="job.description"
      :salary="job.salary"
      :workTime="job.workTime"
      :date="job.date"
      :prerequisites="job.prerequisites"
    ></JobOffer>
  </div>
</template>

<script setup>
import JobOffer from "./JobOffer.vue";
import NavBar from "./NavigationBar.vue";
//Mock data in JSON format
import Mockdata from "../mockdata/joboffers.json";
import { ref, computed, watch } from "vue";

//Suchfunktion
const mockdataRef = ref(Mockdata);
const searchWord = ref("");
const shownJobOffers = computed(() => {
  return mockdataRef.value.filter((job) => {
    const valueString = Object.values(job).join("").toLowerCase();
    return valueString.includes(searchWord.value.toLowerCase());
  });
});

const handleSearch = (newSearchWord) => {
  searchWord.value = newSearchWord;
};
</script>

<style scoped>
.job-offers-container {
  display: flex;
  flex-direction: column;
  align-items: center;
}
</style>
