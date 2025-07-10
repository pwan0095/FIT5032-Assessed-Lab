<template>
  <div class="container mt-5">
    <div class="row">
      <div class="col-md-8 offset-md-2">
        <h1 class="text-center">User Information Form / Credentials</h1>

        <form @submit.prevent="submitForm" class="mt-4">
          <div class="row">
            <div class="col-6">
              <label for="username" class="form-label">Username:</label>
              <input type="text" class="form-control" id="username" v-model="formData.username">
            </div>
            <div class="col-6">
              <label for="password" class="form-label">Password:</label>
              <input type="password" class="form-control" id="password" v-model="formData.password">
            </div>
          </div>

          <div class="form-check mb-3 mt-3">
            <input type="checkbox" class="form-check-input" id="isAustralian" v-model="formData.isAustralian">
            <label class="form-check-label" for="isAustralian">Australian Resident?</label>
          </div>

          <div class="mb-3">
            <label for="reason" class="form-label">Reason For Joining:</label>
            <textarea class="form-control" id="reason" rows="3" v-model="formData.reason"></textarea>
          </div>

          <div class="mb-3">
            <label for="gender" class="form-label">Gender</label>
            <select class="form-select" id="gender" v-model="formData.gender">
              <option value="female">Female</option>
              <option value="male">Male</option>
              <option value="other">Other</option>
            </select>
          </div>

          <div class="text-center">
            <button type="submit" class="btn btn-primary me-2">Submit</button>
            <button type="button" class="btn btn-secondary" @click="clearForm">Clear</button>
          </div>
        </form>
        <div class="row mt-5" v-if="submittedCards.length > 0">
        <div class="d-flex flex-wrap justify-content-start">
            <div v-for="(card, index) in submittedCards" :key="index" class="card m-2" style="width: 18rem;">
                <div class="card-header">
                    User Information
                </div>
                <ul class="list-group list-group-flush">
                    <li class="list-group-item"><strong>Username:</strong> {{ card.username }}</li>
                    <li class="list-group-item"><strong>Password:</strong> {{ card.password }}</li>
                    <li class="list-group-item"><strong>Australian Resident:</strong> {{ card.isAustralian ? 'Yes' : 'No' }}</li>
                    <li class="list-group-item"><strong>Gender:</strong> {{ card.gender }}</li>
                    <li class="list-group-item"><strong>Reason:</strong> {{ card.reason }}</li>
                </ul>
            </div>
        </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue';

// 用于绑定表单输入框的数据
const formData = ref({
  username: '',
  password: '',
  isAustralian: false,
  reason: '',
  gender: 'female'
});

// 新增：一个数组，用来存放所有提交的卡片信息
const submittedCards = ref([]);

// 修改：提交表单时，将当前 formData 的一个副本添加到 submittedCards 数组中
const submitForm = () => {
  // 使用 ... 展开操作符创建一个副本，避免后续修改影响已提交的数据
  submittedCards.value.push({ ...formData.value });
  // 提交后调用清空函数，方便下一次输入
  clearForm();
};

// 清空函数
const clearForm = () => {
  formData.value = {
    username: '',
    password: '',
    isAustralian: false,
    reason: '',
    gender: 'female'
  };
};
</script>

<style scoped>
   .card {
     border: 1px solid #ccc;
     border-radius: 10px;
     box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
   }
   .card-header {
     background-color: #0d6efd; /* 使用 Bootstrap 的主色调 */
     color: white;
     padding: 10px;
     border-radius: 9px 9px 0 0; /* 配合父元素的圆角 */
   }
   .list-group-item {
     padding: 10px;
   }
</style>