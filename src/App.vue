<template>
  <div id="app">
    <DialogConfirm
      :dialogData="dialogData" 
      @closeDialog="toggleDialog" 
      @removeItem="removeItemFromList"
    />
    <Form @submitForm="onFormSubmit" />
    <TotalBalance :list="list" />
    <BudgetList :list="list" @deleteItem="onDeleteItem" />
  </div>
</template>

<script>
import BudgetList from '@/components/BudgetList';
import TotalBalance from '@/components/TotalBalance';
import Form from '@/components/Form';
import DialogConfirm from '@/components/DialogConfirm';

export default {
  name: 'App',
  components: {
   BudgetList,
   TotalBalance,
   Form,
   DialogConfirm
  },
  data: () => ({
    list: {
      1: {
        type: 'INCOME',
        value: 2000,
        comment: 'salary',
        id: 1
      },
      2: {
        type: 'OUTCOME',
        value: 1000,
        comment: 'purchases',
        id: 2
      },
    },
    dialogData: {
      isShow: false,
      listItem: {}
    }
  }),
  methods: {
    toggleDialog() {
      this.dialogData.isShow = !this.dialogData.isShow;
    },
    onDeleteItem(id) {
      this.toggleDialog();
      this.dialogData.listItem = this.list[id];
    },
    removeItemFromList(item) {
      this.$delete(this.list, item.id)
      this.toggleDialog();
    },
    onFormSubmit(formData) {
      const newListItem = {
        ...formData,
        id: Date.now().toString()
      };

      this.$set(this.list, newListItem.id, newListItem);
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
