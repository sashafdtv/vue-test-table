
<template>
  <el-form
    ref="form"
    :model="form"
    :rules="rules"
    label-width="120px">

    <el-form-item
      label="Имя"
      prop="name">
      <el-input v-model="form.name"/>
    </el-form-item>

    <el-form-item
      label="Телефон"
      prop="phone">
      <el-input
        v-model="form.phone"
        type="number">
        <template slot="prepend">+7</template>
      </el-input>
    </el-form-item>

    <el-form-item
      label="Начальник"
      prop="head"
    >
      <el-select
        v-model="form.head"
        placeholder="Выберите руководителя">
        <el-option
          v-for="item in headsList"
          :key="item.id"
          :label="item.name"
          :value="item.id"/>
      </el-select>
    </el-form-item>

    <div class="button-wrapper">
      <el-button
        type="success"
        @click="onSubmit">
        Сохранить
      </el-button>
    </div>
  </el-form>
</template>

<script>
export default {
  name: 'Modal',
  props: {
    value: {
      type: Boolean,
      default: false
    },

    headsList: {
      type: Array,
      default () {
        return []
      }
    }
  },
  data () {
    return {
      /* Данные формы */
      form: {
        name: '',
        phone: '',
        head: ''
      },
      /* Правила валидации */
      rules: {
        name: [
          {required: true, message: 'Пожалуйста, введите имя', trigger: 'blur'}
        ],
        phone: [
          {required: true, message: 'Пожалуйста, введите телефон', trigger: 'blur'},
          {min: 10, max: 10, message: 'Номер телефона должен содержать 11 цифр', trigger: 'blur'}
        ]
      }
    }
  },

  methods: {
    /* Сабмит формы */
    onSubmit () {
      this.$refs['form'].validate(async (valid) => {
        if (valid) {
          /* Отравка данных формы в Table.vue */
          this.$emit('submit', {
            name: this.form.name,
            phone: this.transformNumber(this.form.phone),
            head: this.form.head,
            children: []
          })

          /* Закрываем модалку */
          this.$attrs.close()

          /* Очищаем форму */
          this.$refs['form'].resetFields()
        } else {
          return false
        }
      })
    },

    /* Трансформация номера перед передачей данных вверх */
    transformNumber (number) {
      return '+7' + ' ' + number.slice(0, 3) + ' ' + number.slice(3, 6) + ' ' + number.slice(6, 8) + ' ' + number.slice(8, 10)
    }
  }
}
</script>

<style scoped>

.el-select {
  width: 100%;
}

/* Скрываем стандартные контролы инпута с type="number" */
input::-webkit-outer-spin-button,
input::-webkit-inner-spin-button {
  -webkit-appearance: none;
  margin: 0;
}
</style>
