<template>
  <section>
    <el-table
      :data="tableData"
      style="width: 100%">
      <el-table-column
        prop="name"
        label="Имя"
        width="200"/>
      <el-table-column
        prop="phone"
        label="Телефон"
        width="300"/>
    </el-table>

    <div class="button-wrapper">
      <el-button type="primary">Добавить</el-button>
    </div>
  </section>
</template>

<script>
export default {
  name: 'Table',
  data () {
    return {
      tableData: [{
        name: 'Марина',
        phone: '+7 941 123 21 42'
      }, {
        name: 'Петр',
        phone: '+7 941 123 21 42'
      }, {
        name: 'Алексей',
        phone: '+7 941 123 21 42'
      }, {
        name: 'Борис',
        phone: '+7 941 123 21 42'
      }]
    }
  }
}
</script>

<style scoped>

.el-table {
  margin-bottom: 30px;
  border: 1px solid #EBEEF5
}

.button-wrapper {
  width: 100%;
  display: flex;
  justify-content: center;
}
</style>
