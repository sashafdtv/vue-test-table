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
        @click="changeModalVisibility">Добавить</el-button>
    </div>

    <!-- Модалка -->
    <el-dialog
      :visible.sync="visibleModal"
      title="Добавление пользователя">
      <Form
        @submit="addUser"
      />
    </el-dialog>

  </section>
</template>

<script>
import Form from './Form.vue'

export default {
  name: 'Table',
  components: {
    Form
  },
  data () {
    return {
      visibleModal: false,
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
  },

  methods: {
    /**
     * @param {object} data
     */
    addUser (data) {
      /* Закрываем модалку при сабмите */
      this.visibleModal = false
      return this.tableData.push(data)
    },

    /**
     * Метод меняет видимость модалки (октрывает/закрывает)
     */
    changeModalVisibility () {
      this.visibleModal = !this.visibleModal
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
