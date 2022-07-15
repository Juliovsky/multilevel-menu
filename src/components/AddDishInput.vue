<template>
  <div class="add-input-container">
    <input
      type="text"
      v-model="newMenuValue"
      class="new-dish-input"
      @keydown.enter="addItem"
    />
  </div>
</template>

<script>
export default {
  data() {
    return {
      newMenuValue: "",
    };
  },
  methods: {
    addItem() {
      this.$emit("detect-input-value", this.newMenuValue);
    },
  },
};
</script>

<style scoped>
.new-dish-input {
  display: block;
  margin: 20px;
}
</style>
