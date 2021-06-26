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
        type="number"/>
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
          {min: 11, max: 11, message: 'Номер телефона должен содержать 11 цифр', trigger: 'blur'}
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
