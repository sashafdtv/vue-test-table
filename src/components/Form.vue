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
      <el-input v-model="form.phone"/>
    </el-form-item>

    <el-form-item label="Начальник">
      <el-input v-model="form.head"/>
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
  model: {
    visibleModal: false
  },
  props: {
    value: {
      type: Boolean,
      default: false
    }
  },
  data () {
    return {
      form: {
        name: '',
        phone: '',
        head: ''
      },
      rules: {
        name: [
          {required: true, message: 'Пожалуйста, введите имя', trigger: 'blur'}
        ],
        phone: [
          {required: true, message: 'Пожалуйста, введите телефон', trigger: 'blur'},
          {validator: this.validateNumber, trigger: 'blur'}
        ]
      }
    }
  },

  methods: {
    /* Сабмит формы */
    onSubmit () {
      this.$refs['form'].validate(async (valid) => {
        if (valid) {
          this.$emit('submit', {
            name: this.form.name,
            phone: this.form.phone
          })
        } else {
          return false
        }
      })
    },

    /* Валидация вводимого в форму номера телефона */
    validateNumber (rule, value, callback) {
      if (
        (value.length === 12 && value[0] !== '+') ||
        value.length > 12 ||
        value.length < 11
      ) {
        callback(new Error('Пожалуйста, введите корректный номер телефона'))
      } else {
        callback()
      }
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
</style>
