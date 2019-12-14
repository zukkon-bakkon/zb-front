<template>
  <v-card :loading="loading" class="mx-auto my-12" max-width="374">
    <div v-for="(shop, i) in shops" :key="i">
      <v-img height="250" src="https://cdn.vuetifyjs.com/images/cards/cooking.png"></v-img>

      <v-card-title>{{ shop.name }}</v-card-title>

      <v-card-text>
        <v-row align="center" class="mx-0">
          <v-rating :value="4.5" color="amber" dense half-increments readonly size="14"></v-rating>

          <div class="grey--text ml-4">4.5 (413)</div>
        </v-row>

        <div class="my-4 subtitle-1 black--text">$ • Italian, Cafe</div>

        <div>{{ shop.description }}</div>
      </v-card-text>

      <v-divider class="mx-4"></v-divider>

      <v-card-title>Tonight's availability</v-card-title>

      <v-card-text>
        <v-chip-group v-model="selection" active-class="deep-purple accent-4 white--text" column>
          <v-chip>5:30PM</v-chip>

          <v-chip>7:30PM</v-chip>

          <v-chip>8:00PM</v-chip>

          <v-chip>9:00PM</v-chip>
        </v-chip-group>
      </v-card-text>

      <v-card-actions>
        <v-btn color="deep-purple accent-4" text @click="reserve">Reserve</v-btn>
      </v-card-actions>
    </div>
  </v-card>
</template>

<script>
import axios from "@/plugins/axios";

export default {
  data: () => ({
    loading: false,
    selection: 1,
    shops: []
  }),

  methods: {
    reserve() {
      this.loading = true;

      setTimeout(() => (this.loading = false), 2000);
    }
  },

  async created() {
    try {
      const res = await axios.get("/v1/shops");
      this.shops = res.data;
      console.log("this.shops", this.shops);
    } catch (err) {
      console.log("err", err);
    }
  }
};
</script>

<style>
</style>