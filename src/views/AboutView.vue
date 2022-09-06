<template>
  <div class="about">
    <h1 align="center">Feed</h1>
    <!-- <iframe
      src="https://frans-77.fred.sensetecnic.com/api/monitor"
      width="1000"
      height="800"
    />-->
    <PlanView />
  </div>
</template>

<script>
// @ is an alias to /src
import PlanView from "@/components/PlanView.vue";
//import VolunteerOpp from "@/components/VolunteerOpp.vue";
//import FeedOpp from "@/components/FeedOpp.vue";

export default {
  name: "HomeView",
  components: {
    PlanView,
  },
};
</script>
