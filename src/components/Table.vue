<template>
  <section>
    <!-- Таблица -->
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

    <!-- Кнопка добавления  -->
    <div class="button-wrapper">
      <el-button
        type="primary"
        @click="toggleModal = true">Добавить</el-button>
    </div>

    <!-- Компонент модалки -->
    <Modal :toggle-modal="toggleModal"/>
  </section>
</template>

<script>
import Modal from './Modal.vue'

export default {
  name: 'Table',
  components: {
    Modal
  },
  data () {
    return {
      toggleModal: false,
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
