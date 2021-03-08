<template>
  <div class="container">
    <h1>Registration form</h1>
    <el-form :label-position="'left'" :model="ruleForm" :rules="rules" ref="ruleForm" label-width="160px">

      <el-form-item label="Email" prop="Email" required>
        <el-input v-model="ruleForm.email"></el-input>
      </el-form-item>

      <el-form-item label="Username" prop="Username" required>
        <el-input v-model="ruleForm.username"></el-input>
      </el-form-item>

      <el-form-item label="Password" prop="Password" required>
        <el-input v-model="ruleForm.password" type="password"></el-input>
      </el-form-item>

      <el-form-item label="Birthdate" prop="Birthdate" required>
        <el-date-picker type="date" placeholder="Pick a date" v-model="ruleForm.birthdate"
                        style="width: 100%;"></el-date-picker>
      </el-form-item>

      <el-form-item label="Preferred relationship" prop="Relationship preference">
        <el-radio-group v-model="ruleForm.preference_relationship">
          <el-radio label="Friend"></el-radio>
          <el-radio label="Relationship"></el-radio>
          <el-radio label="Sex"></el-radio>
        </el-radio-group>
      </el-form-item>

      <el-form-item label="Preferred gender" prop="Gender preference">
        <el-radio-group v-model="ruleForm.preference_gender">
          <el-radio label="Male"></el-radio>
          <el-radio label="Female"></el-radio>
          <el-radio label="Both"></el-radio>
        </el-radio-group>
      </el-form-item>

      <el-form-item>
        <el-button type="primary" @click="submitForm('ruleForm')">Register</el-button>
      </el-form-item>

    </el-form>
  </div>
</template>


<script>
export default {
  data() {
    return {
      ruleForm: {
        email: '',
        username: '',
        password: '',
        birthdate: '',
        preference_relationship: '',
        preference_gender: '',
      },
      rules: {
        email: [
          {required: true, pattern: /^\S+@\S+\.\S+$/, message: "Please input correct email address", trigger: 'change'}
        ],
        username: [
          {required: true, message: 'Please input username', trigger: 'blur'},
          {min: 1, max: 150, message: 'Length of the username should be from 1 to 150', trigger: 'change'}
        ],
        password: [
          {required: true, message: 'Please input password', trigger: 'change'}
        ],
        birthdate: [
          {required: true, type: 'date', message: 'Please pick a date', trigger: 'change'}
        ],
        preference_relationship: [
          {required: true, message: 'Please pick preferred relationship', trigger: 'change'}
        ],
        preference_gender: [
          {required: true, message: 'Please pick preferred gender', trigger: 'change'}
        ],
      }
    };
  },
  methods: {
    submitForm(formName) {
      this.$refs[formName].validate((valid) => {
        if (valid) {
          let data = {
            email: this.email,
            username: this.username,
            password: this.password,
            birthdate: this.birthdate,
            preference_relationship: this.preference_relationship,
            preference_gender: this.preference_gender,
          }
          this.$store.dispatch('register', data)
              .then(() => this.$router.push('/'))
              .catch(err => console.log(err))
        } else {
          console.log('Input data is not validated');
          return false;
        }
      });
    },
  }
}
</script>

<style lang="scss" scoped>
h1 {
  padding-bottom: 30px;
}
</style>