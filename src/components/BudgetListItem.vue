<template>
  <div class="list-item">
    <div>
      <i class="el-icon-top" v-if="item.type === 'INCOME'"></i>
      <i class="el-icon-bottom" v-else></i>
    </div>
    <div class="budget-comment">{{ item.comment }}</div>
    <div class="budget-value" :style="{color: setColorValue}">{{ item.value }}</div>
    <ElButton 
      type="danger" 
      size="mini" 
      @click="onDeleteItem(item.id)"
    >
      Delete
    </ElButton>
  </div>
</template>

<script>
export default {
  name: 'BudgetList',
  props: {
    item: {
      type: Object,
      default: () => ({})
    }
  },
  computed: {
    setColorValue() {
      return this.item.type === "INCOME" ? "green" : "red";
    }
  },
  methods: {
    onDeleteItem(id) {
      this.$emit('deleteItem', id);
    }
  }
}
</script>

<style scoped>
.list-item {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 10px 15px;
}
.budget-value {
  font-weight: bold;
  margin-left: auto;
  margin-right: 20px;
}
.budget-comment{
  text-align: left;
}
</style>