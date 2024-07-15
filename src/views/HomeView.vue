<script setup>
import Hero from '@/components/Hero.vue';
import HomeCard from '@/components/HomeCards.vue';
import JobListings from '@/components/JobListings.vue';
</script>

<template>
  <Hero />
  <HomeCard />
  <JobListings :limit="3" :showButton="true"/>
</template>
