<template>
  <div class="services">
    <div class="services--main">
      <h1>Services</h1>
      <div class="services--main-box">
        <div
          v-for="({ price, title, toggle }, index) in servicesItems"
          :class="{ active: toggle }"
          @click="addTotal(index)"
          class="service--box"
          :key="index"
        >
          <h3>{{ title }}</h3>
          <h3>${{ price }}</h3>
        </div>
      </div>
      <div class="line"></div>
      <div class="total">
        <h3>Total:</h3>
        <h3>${{ total }}</h3>
      </div>
    </div>
  </div>
</template>

<style lang="scss">
@import "../styles/services.scss";
</style>

<script lang="ts">
import { defineComponent } from "vue";

export default defineComponent({
  name: "HomeView",
  data: () => ({
    total: 0,
    servicesItems: [
      {
        title: "Web Development",
        price: 300,
        toggle: false,
      },
      {
        title: "Design",
        price: 400,
        toggle: false,
      },
      {
        title: "Interigation",
        price: 250,
        toggle: false,
      },
      {
        title: "Training",
        price: 220,
        toggle: false,
      },
    ],
  }),
  methods: {
    addTotal(index: number) {
      this.servicesItems[index].toggle = !this.servicesItems[index].toggle;
      if (this.servicesItems[index].toggle) {
        this.total += this.servicesItems[index].price;
      } else {
        this.total -= this.servicesItems[index].price;
      }
    },
  },
});
</script>
