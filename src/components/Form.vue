
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

    <el-form-item label="Начальник">
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
      type: Object,
      default () {
        return {}
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
            phone: this.form.phone,
            head: this.form.head,
            children: []
          })

          /* Обнуляем значения form */
          for (let prop in this.form) {
            this.form[prop] = ''
          }
        } else {
          return false
        }
      })
    }
  }
}
</script>

<style>
.button-wrapper {
  width: 100%;
  display: flex;
  justify-content: center;
}

/* Скрываем стандартные контролы инпута с type="number" */
input::-webkit-outer-spin-button,
input::-webkit-inner-spin-button {
  -webkit-appearance: none;
  margin: 0;
}
</style>
