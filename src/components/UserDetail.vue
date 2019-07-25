<template>
  <div class="component">
    <h3>You may view the User Details here</h3>
    <p>Many Details</p>
    <p>Username: {{ name }}</p>
    <p>Age: {{userAge}}</p>
    <button @click="resetName">Reset Name</button>
    <button @click="resetfn()">Reset via callback</button>
  </div>
</template>

<script>
import { eventBus } from "../main";
export default {
  props: {
    userAge: {
      type: Number
    },
    name: {
      type: String
    },
    resetfn: { type: Function }
  },
  methods: {
    switchName() {
      return this.name
        .split("")
        .reverse()
        .join();
    },
    resetName() {
      this.name = "Stan";
      this.$emit("nameWasReset", this.name);
    }
  },
  created() {
    eventBus.$on("ageWasEdited",age=>this.userAge=age);
  }
};
</script>

<style scoped>
div {
  background-color: lightcoral;
}
</style>
