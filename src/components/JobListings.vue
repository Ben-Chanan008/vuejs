<script setup>
import jobData from '@/jobs.json';
import { ref, reactive, defineProps, onMounted } from 'vue';
import { RouterLink } from 'vue-router';
import PulseLoader from 'vue-spinner/src/PulseLoader.vue';
import JobListing from "@/components/JobListing.vue";
import axios from 'axios';

defineProps({
  limit: Number,
  showButton: {
    type: Boolean,
    default: false
  }
})

const state = reactive({
  jobs: [],
  isLoading: true
});

onMounted(async () => {
  try{
    const response = await axios.get('/api/jobs');
    state.jobs = response.data;

    state.isLoading = false;
  } catch(e) {
    console.error('Error fetching jobs', e);
  }
})
</script>

<template>
  <section class="bg-blue-50 px-4 py-10">
    <div class="container-xl lg:container m-auto">
      <h2 class="text-3xl font-bold text-green-500 mb-6 text-center">Browse Jobs</h2>
      <div v-if="state.isLoading" class="text-center py-6">
        <PulseLoader />
      </div>
      <div v-else class="grid grid-cols-1 md:grid-cols-3 gap-6">
        <JobListing v-for="job in state.jobs.slice(0, limit || state.jobs.length)" :key="job.id" :job="job"/>
      </div>
    </div>
  </section>
  <section v-show="showButton" class="m-auto max-w-lg my-10 px-6">
    <RouterLink to="/jobs" class="block bg-black text-white text-center py-4 px-6 rounded-xl hover:bg-gray-700">View All Jobs</RouterLink>
  </section>
</template>
