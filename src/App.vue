<template>
  <div class="tale-box">
    <div class="title">CRUD Demo</div>
  <div class="query-box">
    <el-input v-model="queryInput" placeholder="Please input" />
    <el-button type="primary">Primary</el-button>
  </div>
  <el-table ref="multipleTableRef" :data="tableData" style="width: 100%" border @selection-change="handleSelectionChange">
    <el-table-column type="selection" width="55" />
    <el-table-column fixed prop="date" label="Date" width="150" />
    <el-table-column prop="name" label="Name" width="120" />
    <el-table-column prop="state" label="State" width="120" />
    <el-table-column prop="city" label="City" width="120" />
    <el-table-column prop="address" label="Address" width="600" />
    <el-table-column prop="zip" label="Zip" width="120" />
    <el-table-column fixed="right" label="Operations" width="120">
      <template #default>
        <el-button link type="primary" size="small" @click="handleClick"
          >Detail</el-button
        >
        <el-button link type="primary" size="small">Edit</el-button>
      </template>
    </el-table-column>
  </el-table>
 </div>
</template>
<script setup>
import { ref } from "vue";

let queryInput = ref('')

const multipleSelection=ref([])

const handleClick = () => {
  console.log('click')
}

const handleSelectionChange = (val) => {
  multipleSelection.value = val
  console.log(val);
}

const tableData = [
  {
    date: '2016-05-03',
    name: 'Tom',
    state: 'California',
    city: 'Los Angeles',
    address: 'No. 189, Grove St, Los Angeles',
    zip: 'CA 90036',
    tag: 'Home',
  },
  {
    date: '2016-05-02',
    name: 'Tom',
    state: 'California',
    city: 'Los Angeles',
    address: 'No. 189, Grove St, Los Angeles',
    zip: 'CA 90036',
    tag: 'Office',
  },
  {
    date: '2016-05-04',
    name: 'Tom',
    state: 'California',
    city: 'Los Angeles',
    address: 'No. 189, Grove St, Los Angeles',
    zip: 'CA 90036',
    tag: 'Home',
  },
  {
    date: '2016-05-01',
    name: 'Tom',
    state: 'California',
    city: 'Los Angeles',
    address: 'No. 189, Grove St, Los Angeles',
    zip: 'CA 90036',
    tag: 'Office',
  },
]
</script>

<style scoped>

.tale-box{
  margin: 170px auto;
  width: 800px;
}
.query-box{
  display: flex;
  justify-content: space-between;
  margin-bottom: 20px;
}
.title{
  text-align: center;
  margin-bottom: 20px;
}
.el-input{
    width: 300px;

}
</style>
