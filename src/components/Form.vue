<template>
  <el-card class="form-card">
    <el-form
      :model="formData"
      ref="addItemForm"
      :rules="rules"
      label-position="top"
    >
      <el-form-item label="Type" prop="type">
        <el-select
          class="type-select"
          v-model="formData.type"
          placeholder="Choose type..."
        >
          <el-option label="Income" value="INCOME" />
          <el-option label="Outcome" value="OUTCOME" />
        </el-select>
      </el-form-item>
      <el-form-item label="Date" prop="date">
        <el-date-picker
          type="date"
          format="d.MM"
          value-format="d.MM"
          placeholder="Pick a date"
          v-model="formData.date"
        ></el-date-picker>
      </el-form-item>
      <el-form-item label="Comments" prop="comment">
        <el-input v-model="formData.comment" />
      </el-form-item>
      <el-form-item label="Value" prop="value">
        <el-input v-model.number="formData.value" />
      </el-form-item>
      <el-button @click="onSubmit" type="primary">Submit</el-button>
    </el-form>
  </el-card>
</template>

<script>
export default {
  name: "Form",
  data() {
    const checkValue = (rule, value, callback) => {
      if (value === 0) {
        return callback(new Error("Введите значение больше 0"));
      } else {
        callback();
      }
    };

    return {
      formData: {
        type: "INCOME",
        date: "",
        comment: "",
        value: 0
      },
      rules: {
        type: [
          { required: true, message: "Please select type", trigger: "blur" }
        ],
        date: [
          { required: true, message: "Please select date", trigger: "change" }
        ],
        comment: [
          { required: true, message: "Please input comment", trigger: "change" }
        ],
        value: [
          { required: true, message: "Please input value", trigger: "change" },
          {
            type: "number",
            message: "Value must be a number",
            trigger: "change"
          },
          { validator: checkValue, trigger: "change" }
        ]
      }
    };
  },

  methods: {
    onSubmit() {
      this.$refs.addItemForm.validate(valid => {
        if (valid) {
          this.$emit("submitForm", { ...this.formData });
          this.$refs.addItemForm.resetFields();
        }
      });
    }
  }
};
</script>

<style scoped>
.form-card {
  max-width: 500px;
  margin: auto;
  text-align: left;
}

.type-select {
  width: 100%;
}
</style>
