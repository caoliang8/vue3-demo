<template>
  <div class="tale-box">
    <div class="title">CRUD Demo</div>
  <div class="query-box">
    <el-input class="query-input" v-model="queryInput" placeholder="Please input" />
    <div class="btn-list">
          <el-button type="primary" @click="handleAdd">增加</el-button>
    <el-button type="danger" @click="handleDellList" v-if="multipleSelection.length>0">多选删除</el-button>

    </div>
  </div>
  <el-table ref="multipleTableRef" :data="tableData" style="width: 100%" border @selection-change="handleSelectionChange">
    <el-table-column type="selection" width="55" />
    <el-table-column prop="name" label="姓名" width="120" />
    <el-table-column prop="email" label="邮箱" width="120" />
    <el-table-column prop="phone" label="手机" width="120" />
    <el-table-column prop="status" label="状态" width="120" />
    <el-table-column prop="address" label="地址" width="300" />
    <el-table-column fixed="right" label="操作" width="120">
      <template #default="scope">
        <el-button link type="primary" size="small" @click="handleRowDel(scope.row)" style="color: #f56c6c;"
          >删除</el-button>
        <el-button link type="primary" size="small" @click="handleEdit(scope.row)">编辑</el-button>
      </template>
    </el-table-column>
  </el-table>

    <!-- dialog -->
    <el-dialog v-model="dialogFormVisible" :title="dialogType==='add'?'新增':'编辑'">
    <el-form :model="tableForm">
      <el-form-item label="姓名" :label-width="60">
        <el-input v-model="tableForm.name" autocomplete="off" />
      </el-form-item>
      <el-form-item label="邮箱" :label-width="60">
        <el-input v-model="tableForm.email" autocomplete="off" />
      </el-form-item>
      <el-form-item label="电话" :label-width="60">
        <el-input v-model="tableForm.phone" autocomplete="off" />
      </el-form-item>
      <el-form-item label="状态" :label-width="60">
        <el-input v-model="tableForm.status" autocomplete="off" />
      </el-form-item>
      <el-form-item label="地址" :label-width="60">
        <el-input v-model="tableForm.address" autocomplete="off" />
      </el-form-item>

    </el-form>
    <template #footer>
      <span class="dialog-footer">
        <el-button type="primary" @click="dialogConfirm">
          确认
        </el-button>
      </span>
    </template>
  </el-dialog>
 </div>
</template>
<script setup>
import { ref } from "vue";

let queryInput = $ref('')  //viteconfig.js设置开启$
const tableData = $ref([
  {
    id:"1",
    name: 'Tom',
    email: '123@qq.com',
    phone:'13f8',
    status: 'California',
    address: 'No. 189, Grove St, Los Angeles',
  },
  {
    id:"2",
    name: 'Tom2',
    email: '123@qq.com',
    phone:'1338',
    status: 'California',
    address: 'No. 189, Grove St, Los Angeles',
  },
  {
    id:"3",
    name: 'Tom3',
    email: '123@qq.com',
    phone:'13f8',
    status: 'California',
    address: 'No. 189, Grove St, Los Angeles',
  },
  {
    id:"4",
    name: 'Tom4',
    email: '123@qq.com',
    phone:'13f8',
    status: 'California',
    address: 'No. 189, Grove St, Los Angeles',
  },
])

let multipleSelection = $ref([])
let dialogFormVisible = $ref(false)
let tableForm = $ref({
  name: '张三',
  email: '33',
  phone: '22',
  status: '在职',
  address:'aafa'
})
let dialogType=$ref('add')
// 方法
const handleEdit = (row) => {
  dialogFormVisible = true
  dialogType = 'edit'
  tableForm={...row}
}
const handleRowDel = ({id}) => {
  console.log(id)
  let index = tableData.findIndex(item => item.id === id)
  tableData.splice(index,1)
}

let handleSelectionChange = (val) => {
  // multipleSelection.value = val
    //  multipleSelection= val
  // console.log(val);

  multipleSelection=[]
  val.forEach(item => {
    multipleSelection.push(item.id)
  })

}
const handleAdd = () => {
  // dialogFormVisible.value=true
  dialogFormVisible = true    //开启$,去掉.value
  tableForm = {}
  //dialogType="add"
}
const dialogConfirm = () => {
  dialogFormVisible = false
  //判断是编辑还是新增
  if (dialogType === 'add') {
      tableData.push({
        id:(tableData.length +1).toString(),
        ...tableForm,
      })
  } else {
    //获取到当前的这条索隐
    let index = tableData.findIndex(item => item.id === tableForm.id)
    tableData[index]=tableForm
  }


}
const handleDellList = () => {
  multipleSelection.forEach(id => {
    handleRowDel({id})
  })
  multipleSelection=[]
}

</script>

<style scoped>

.tale-box{
  margin: 200px auto;
  width: 800px;
}
.tale-box .query-box{
  display: flex;
  justify-content: space-between;
  margin-bottom: 20px;
}
.title{
  text-align: center;
  margin-bottom: 20px;
}
.query-input{
    width: 300px;

}
</style>
