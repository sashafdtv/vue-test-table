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
        :headsList="tableData"
        @submit="submitHandler"
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
        id: '1',
        name: 'Марина',
        phone: '+7 941 123 21 42',
        children: []
      }, {
        id: '2',
        name: 'Петр',
        phone: '+7 941 123 21 42',
        children: []
      }, {
        id: '3',
        name: 'Алексей',
        phone: '+7 941 123 21 42',
        children: []
      }, {
        id: '4',
        name: 'Борис',
        phone: '+7 941 123 21 42',
        children: []
      }]
    }
  },

  methods: {
    /* Хэндлер сабмита формы */
    submitHandler (data) {
      /* После сабмита закрываем модалку */
      this.changeModalVisibility()
      this.addUser(data)
    },

    /* Добавление нового пользователя */
    addUser (data) {
      /* Приводим телефон к нужному формату */
      data.phone = this.transformNumber(data.phone)
      if (data.head) {
        const headUser = this.tableData.find(user => user.id === data.head)
        /* id дочернего юзера формируется с префиксом родельского */
        data.id = headUser.id + '-' + (+headUser.children.length + 1)
        return headUser.children.push(data)
      } else {
        data.id = this.tableData.length + 1
        return this.tableData.push(data)
      }
    },

    /* Трансформация номера перед добавлением в модель */
    transformNumber (number) {
      return '+7' + ' ' + number.slice(0, 3) + ' ' + number.slice(3, 6) + ' ' + number.slice(6, 8) + ' ' + number.slice(8, 10)
    },

    /* Метод меняет видимость модалки (октрывает/закрывает) */
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
