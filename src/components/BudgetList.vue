<template>
  <div class="budget-list-wrap">
    <ElCard :header="header">
      <ElButton type="primary" size="mini" plain @click="sortList('ALL')">
        all
      </ElButton>
      <ElButton type="primary" size="mini" plain @click="sortList('INCOME')">
        coming
      </ElButton>
      <ElButton type="primary" size="mini" plain @click="sortList('OUTCOME')">
        consumption
      </ElButton>

      <transition name="block">
        <template v-if="isEmpty">
          <transition-group name="list" tag="div">
            <BudgetListItem
              v-for="(item, key) in filterList"
              :key="key"
              :item="item"
              @deleteItem="deleteItem"
            />
          </transition-group>
        </template>
        <ElAlert v-else type="info" :title="emptyTitle" :closable="false" />
      </transition>
    </ElCard>
  </div>
</template>

<script>
import BudgetListItem from './BudgetListItem';

export default {
  name: 'BudgetList',
  components: {
    BudgetListItem
  },
  props: {
    list: {
      type: Object,
      default: () => ({})
    }
  },
  data: () => ({
    header: "Budget List",
    emptyTitle: "List is empty!",
    filterList: null
  }),
  computed: {
    isEmpty() {
      return !!Object.keys(this.list).length;
    }
  },
  created() {
    this.filterList = this.list;
  },
  methods: {
    deleteItem(id) {
      this.$emit("deleteItem", id);
    },
    sortList(sortName) {
      if (sortName === 'ALL') {
        this.filterList = this.list;
      }
      if (sortName === 'INCOME') {
        this.filterList = Object.values(this.list).filter(item => item.type === 'INCOME');
      }
      if (sortName === 'OUTCOME') {
        this.filterList = Object.values(this.list).filter(item => item.type === 'OUTCOME');
      }
    }
  }
}
</script>

<style scoped>
.budget-list-wrap {
  max-width: 500px;
  margin: auto;
}
.block-enter-active, .block-leave-active {
  transition: all 0.8s;
}
.block-enter, .block-leave-to {
  opacity: 0;
  transform: translateY(30px);
}
.list-enter-active, .list-leave-active {
  transition: all 0.8s;
}
.list-enter, .list-leave-to {
  opacity: 0;
  transform: translateX(30px);
}
</style>
