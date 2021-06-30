<template>
  <div id="app">
    <!-- Таблица -->
    <Table :tableData = "tableData"/>

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
        :close="closeHandler"
        @submit="submitHandler">
        />
    </form></el-dialog>
  </div>
</template>

<script>
import Table from './components/Table'
import Form from './components/Form.vue'

export default {
  name: 'App',
  components: {
    Table,
    Form
  },

  data () {
    return {
      visibleModal: false
    }
  },

  computed: {
    tableData: function () {
      return this.loadData('tableData') ||
      [{
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
    /* Метод меняет видимость модалки (октрывает/закрывает) */
    changeModalVisibility () {
      this.visibleModal = !this.visibleModal
    },

    /* Метод добавление нового пользователя */
    addUser (data) {
      if (data.head) {
        const headUser = this.tableData.find(user => user.id === data.head)
        /* id дочернего юзера формируется с префиксом родельского */
        data.id = headUser.id + '-' + (+headUser.children.length + 1)
        headUser.children.push(data)
      } else {
        data.id = this.tableData.length + 1
        this.tableData.push(data)
      }
      /* Сохраняем данные таблицы */
      this.saveData('tableData', this.tableData)
    },

    /* Хэндлер закрытия модалки */
    closeHandler () {
      this.changeModalVisibility()
    },

    /* Хэндлер сабмита модалки */
    submitHandler (data) {
      this.addUser(data)
    },

    /* Получение данных */
    loadData (name) {
      try {
        return JSON.parse(localStorage.getItem(name))
      } catch (error) {
        return false
      }
    },

    /* Сохранение данных */
    saveData (name, data) {
      return localStorage.setItem(name, JSON.stringify(data))
    }
  }
}
</script>

<style>

body {
  margin: 0;
  height: 100vh;
  width: 100%;
  display: flex;
  justify-content: center;
  align-items: center;
}

.button-wrapper {
  width: 100%;
  display: flex;
  justify-content: center;
}

</style>
