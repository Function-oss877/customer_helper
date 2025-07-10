<template>
  <div class="register-container">
    <h2>用户注册</h2>
    <form @submit.prevent="handleSubmit" class="register-form">
      <!-- 用户名 -->
      <div class="form-group">
        <label for="username">用户名</label>
        <input
          type="text"
          id="username"
          v-model="form.username"
          @blur="validateUsername"
          placeholder="请输入4-16位用户名"
        />
        <span class="error-message" v-if="errors.username">{{ errors.username }}</span>
      </div>

      <!-- 性别 -->
      <div class="form-group">
        <label>性别</label>
        <div class="radio-group">
          <label>
            <input
              type="radio"
              v-model="form.gender"
              value="male"
              checked
            /> 男
          </label>
          <label>
            <input
              type="radio"
              v-model="form.gender"
              value="female"
            /> 女
          </label>
        </div>
      </div>

      <!-- 手机号 -->
      <div class="form-group">
        <label for="phone">手机号</label>
        <input
          type="text"
          id="phone"
          v-model="form.phone"
          @blur="validatePhone"
          placeholder="请输入11位手机号"
        />
        <span class="error-message" v-if="errors.phone">{{ errors.phone }}</span>
      </div>

      <!-- 邮箱 -->
      <div class="form-group">
        <label for="email">邮箱</label>
        <input
          type="email"
          id="email"
          v-model="form.email"
          @blur="validateEmail"
          placeholder="请输入有效邮箱地址"
        />
        <span class="error-message" v-if="errors.email">{{ errors.email }}</span>
      </div>

      <button type="submit" class="submit-btn" :disabled="isSubmitting">
        {{ isSubmitting ? '注册中...' : '立即注册' }}
      </button>
    </form>
  </div>
</template>

<script>
export default {
  name: 'RegisterPage',
  data() {
    return {
      form: {
        username: '',
        gender: 'male',
        phone: '',
        email: ''
      },
      errors: {
        username: '',
        phone: '',
        email: ''
      },
      isSubmitting: false
    }
  },
  methods: {
    validateUsername() {
      if (!this.form.username.trim()) {
        this.errors.username = '用户名不能为空'
      } else if (this.form.username.length < 1 || this.form.username.length > 16) {
        this.errors.username = '用户名长度应小于16个字符'
      } else {
        this.errors.username = ''
      }
    },
    validatePhone() {
      const phoneReg = /^1[3-9]\d{9}$/
      if (!this.form.phone) {
        this.errors.phone = '手机号不能为空'
      } else if (!phoneReg.test(this.form.phone)) {
        this.errors.phone = '请输入有效的手机号'
      } else {
        this.errors.phone = ''
      }
    },
    validateEmail() {
      const emailReg = /^[^\s@]+@[^\s@]+\.[^\s@]+$/
      if (!this.form.email) {
        this.errors.email = '邮箱不能为空'
      } else if (!emailReg.test(this.form.email)) {
        this.errors.email = '请输入有效的邮箱地址'
      } else {
        this.errors.email = ''
      }
    },
    validateForm() {
      this.validateUsername()
      this.validatePhone()
      this.validateEmail()
      
      return !this.errors.username && !this.errors.phone && !this.errors.email
    },
    handleSubmit() {
      if (this.validateForm()) {
        this.isSubmitting = true
        
        // 模拟API请求
        setTimeout(() => {
          console.log('注册信息:', this.form)
          alert('注册成功!')
          this.isSubmitting = false
          
          // 实际项目中替换为真实的API调用
          // this.$axios.post('/api/register', this.form)
          //   .then(response => {
          //     alert('注册成功!')
          //     this.isSubmitting = false
          //   })
          //   .catch(error => {
          //     alert('注册失败: ' + error.message)
          //     this.isSubmitting = false
          //   })
        }, 1500)
      }
    }
  }
}
</script>

<style scoped>
.register-container {
  max-width: 500px;
  margin: 40px auto;
  background: white;
  padding: 30px;
  border-radius: 8px;
  box-shadow: 0 0 20px rgba(0, 0, 0, 0.1);
}

h2 {
  text-align: center;
  color: #333;
  margin-bottom: 25px;
  font-size: 24px;
}

.register-form {
  display: flex;
  flex-direction: column;
}

.form-group {
  margin-bottom: 20px;
}

label {
  display: block;
  margin-bottom: 8px;
  font-weight: bold;
  color: #555;
}

input[type="text"],
input[type="email"] {
  width: 100%;
  padding: 10px;
  border: 1px solid #ddd;
  border-radius: 4px;
  box-sizing: border-box;
  font-size: 16px;
  transition: border 0.3s;
}

input[type="text"]:focus,
input[type="email"]:focus {
  border-color: #4CAF50;
  outline: none;
}

.radio-group {
  display: flex;
  gap: 20px;
  margin-top: 8px;
}

.radio-group label {
  display: flex;
  align-items: center;
  font-weight: normal;
  cursor: pointer;
  color: #333;
}

.radio-group input[type="radio"] {
  margin-right: 8px;
}

.error-message {
  color: #e74c3c;
  font-size: 13px;
  display: block;
  margin-top: 5px;
}

.submit-btn {
  background-color: #4CAF50;
  color: white;
  padding: 12px;
  border: none;
  border-radius: 4px;
  cursor: pointer;
  font-size: 16px;
  margin-top: 15px;
  transition: background-color 0.3s;
}

.submit-btn:hover {
  background-color: #45a049;
}

.submit-btn:disabled {
  background-color: #cccccc;
  cursor: not-allowed;
}
</style>