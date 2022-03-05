<template>
  <div class="items-center">
    <el-button type="danger" @click="Createnew">Tạo mới</el-button>
    <el-button type="success" @click="lamthu">Làm thử</el-button>
    <el-table :data="tableData" style="width: 100%">
      <el-table-column label="Id" width="50px">
        <template slot-scope="{ row }">
          {{ row.id }}
        </template>
      </el-table-column>

      <el-table-column label="Nội dung câu hỏi" width="150px">
        <template slot-scope="{ row }">
          {{ row.question.content }}
        </template>
      </el-table-column>

      <el-table-column label="" width="100px">
        <template slot-scope="{ row }">
          <el-button type="primary" @click="update(row.id)">Sửa</el-button>
        </template>
      </el-table-column>

      <el-table-column>
        <template slot-scope="{ row }">
          <el-button type="danger" @click="deleteData(row.id)">Xóa</el-button>
        </template>
      </el-table-column>
    </el-table>
  </div>
</template>

  <script>
import axios from 'axios'
export default {
  name: 'IndexPage',
  data() {
    return {
      tableData: [],
    }
  },
  created() {
    this.getdata()
  },
  methods: {
    getdata() {
      this.tableData = []
      axios
        .get('https://6214967f89fad53b1f17fd73.mockapi.io/api/noitu/q')
        .then((res) => {
          this.tableData = res.data
        })
    },
    update(id) {
      this.$router.push('/update/' + id)
    },
    deleteData(id) {
      axios
        .delete('https://6214967f89fad53b1f17fd73.mockapi.io/api/noitu/q/' + id)
        .then((res) => {
          this.getdata()
          this.$message({
            message: 'Đã xóa thành công ',
            type: 'success',
          })
        })
    },
    Createnew() {
      this.$router.push('/test')
    },
     lamthu() {
      this.$router.push('/lamthu')
    },
  },
}
</script>
