<template>
  <v-layout
    row
    fill-hieght
    justify-space-around
  >
    <v-flex ml-3>
      <v-card-title primary-title>
        <div>
          <h3 class="text-sm-center">Activities</h3>
          <v-timeline>
            <v-timeline-item
              v-for="(activity, i) in activities"
              :key="i"
              small
            >
              <template>
                <span v-text="activity.created_at"></span>
              </template>
              <div class="py-3">
                <div style="min-width: 700px; ">
                  {{activity.causer.name}} {{activity.description}} {{activity.properties.attributes.name }}
                </div>
              </div>
            </v-timeline-item>
          </v-timeline>
        </div>
      </v-card-title>
    </v-flex>
  </v-layout>
</template>


<script>
export default {
  name: "Activities",
  data: () => ({
    activities: []
  }),
  created() {
    axios.get("api/activities").then(response => {
      this.activities = response.data;
    });
  }
};
</script>
<style>
.theme--light.v-timeline:before {
  background: rgba(76, 12, 228, 0.12);
  left: 395px;
}
</style>
