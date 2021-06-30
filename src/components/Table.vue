<template>
  <section>
    <!-- Таблица -->
    <el-table
      :data="tableData"
      style="width: 100%"
      row-key="id">
      <el-table-column
        prop="name"
        label="Имя"
        width="200"
        sortable/>
      <el-table-column
        prop="phone"
        label="Телефон"
        width="300"/>
    </el-table>

  </section>
</template>

<script>
export default {
  name: 'Table',

  props: {
    tableData: {
      type: Array,
      default: () => []
    }
  }
}
</script>

<style scoped>
.el-table {
  margin-bottom: 30px;
  border: 1px solid #EBEEF5
}
</style>
