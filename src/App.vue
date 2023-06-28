<template>
  <div class="tale-box">
    <div class="title">CRUD Demo</div>
 
  <div class="query-box">
    <el-input v-model="queryInput" placeholder="Please input" />
    <el-button type="primary">Primary</el-button>
  </div>
 </div>
</template>
<script setup>
import { ref } from "vue";

let queryInput=ref('')
</script>


<style scoped>
.title{
  text-align: center;
}
</style>
