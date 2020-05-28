<template>
  <div class="total-value" :style="{color: balanceColor}">
    Balance: {{ total }}
  </div>
</template>

<script>
export default {
  name: "TotalBalance",
  props: {
    list: {
      type: Object,
      default: () => ({})
    }
  },
  computed: {
    total() {
      return Object.values(this.list).reduce((acc, item) => {
        if (item.type === "INCOME") {
          return acc + item.value;
        }
        return acc - item.value;
      }, 0);
    },
    balanceColor() {
      if (this.total > 0) return "green";
      if (this.total === 0) return "black";
      return "red";
    }
  }
}
</script>

<style scoped>
.total-value {
  font-size: 26px;
  text-transform: uppercase;
  padding: 20px;
  text-align: center;
}
</style>