<template>
  <ElDialog
    title="Tips"
    :visible.sync="dialogData.isShow"
    width="30%"
    :before-close="dialogClose">
    <span>Do you really want to delete?</span>
    <div>{{dialogData.listItem.comment}} {{dialogData.listItem.value}}</div>
    <span slot="footer" class="dialog-footer">
      <ElButton @click="dialogClose">Cancel</ElButton>
      <ElButton @click="dialogConfirm" type="primary">Confirm</ElButton>
    </span>
  </ElDialog>
</template>

<script>
  export default {
    name: 'DialogConfirm',
    props: ['dialogData'],
    methods: {
      dialogClose() {
        this.$emit('closeDialog')
      },
      dialogConfirm() {
        this.$emit('removeItem', this.dialogData.listItem)
      }
    }
  };
</script>