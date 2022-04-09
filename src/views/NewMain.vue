<template>
  <div>
    <v-container>
      <v-row>
        <v-col
          v-for="(value, index) in stepsData"
          :key="index"
          cols="12"
          sm="4"
        >
          <steps :title="value.title" :subtitle="value.description" :link="`/new-container/stepper?id=${index + 1}`"/>
        </v-col>
      </v-row>
    </v-container>
  </div>
</template>

<script>
import Steps from "@/components/Steps";

export default {
  data: () => ({
    stepsData: [
      {
        title: "Step 1",
        description:
          "Define your CURRENT container terminal data and assumption",
      },
      {
        title: "Step 2",
        description: "Check your CURRENT container terminal capacity",
      },
      {
        title: "Step 3",
        description: "Define your TARGET parameter",
      },
      {
        title: "Step 4",
        description: "Check your TARGET container terminal capacity",
      },
      {
        title: "Step 5",
        description: "Check the ANALYSIS RESULT",
      },
      {
        title: "Step 6",
        description:
          "Input Operational Cost-Related Assumptions and Check Operational Cost Impacts",
      },
      {
        title: "Step 7",
        description:
          "Input Investment Cost-Related Assumptions and Check Operational Cost Impacts",
      },
      {
        title: "Step 8",
        description: "Check the diagnosis summary",
      },
    ],
  }),
  components: {
    Steps,
  },
};
</script>

<style>
</style>