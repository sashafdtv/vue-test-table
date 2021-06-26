<template>
  <el-dialog
    :visible.sync="toggleModal"
    title="Добавление пользователя">

    <el-form
      ref="form"
      :model="form"
      label-width="120px">

      <el-form-item label="Имя">
        <el-input v-model="form.name"/>
      </el-form-item>

      <el-form-item label="Телефон">
        <el-input v-model="form.phone"/>
      </el-form-item>

      <el-form-item label="Начальник">
        <el-input v-model="form.head"/>
      </el-form-item>

    </el-form>

  </el-dialog>
</template>

<script>
export default {
  name: 'Modal',
  props: {
    toggleModal: {
      type: [Boolean],
      default: true
    }
  },
  data () {
    return {
      form: {
        name: '',
        phone: '',
        head: ''
      }
    }
  },
  methods: {
    onSubmit () {
      console.log('submit!')
    }
  }
}
</script>

<style>

</style>
§
