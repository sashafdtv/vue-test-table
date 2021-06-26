<template>
  <el-dialog
    :visible.sync="toggleModal"
    title="Shipping address">
    <p>Тело модалки</p>
  </el-dialog>
</template>

<script>
export default {
  name: 'Modal',
  props: {
    toggleModal: {
      type: [Boolean],
      default: true
    }
  }
}
</script>

<style>

</style>
