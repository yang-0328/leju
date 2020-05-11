<template>
  <!-- class名字 文件名+ -main -->
  <div class="clazz-main">
    <el-card class="box-card my-card search-block">
      <div slot="header" class="clearfix">
        <span>搜索条件</span>
      </div>
      <el-row>
        <el-col :span="6">
          <el-input v-model="search.className" size="small" placeholder="班级名称"></el-input>
        </el-col>
        <el-col :span="6">
          <el-input v-model="search.startTime" size="small" placeholder="开班时间"></el-input>
        </el-col>
      </el-row>
      <el-row>
          <el-col :span="6">
              <el-button type="primary"  size="small" @click="doSearch" >搜索</el-button>
          </el-col>
      
      </el-row>
      
    </el-card>
    <el-card class="my-card">
        <div slot="header">
            <span>数据内容</span>
        </div>
       
<el-table :data="classList" border style="width: 100%">
      <el-table-column type="index" fixed width="50"></el-table-column>
      <el-table-column prop="className" fixed label="班级名称" width="180"></el-table-column>
      <el-table-column prop="type" label="班级类型" width="180"></el-table-column>
      <el-table-column prop="desc" label="班级描述" width="180"></el-table-column>
      <el-table-column prop="startTime" label="开班时间"></el-table-column>
      <el-table-column prop="endTime" label="结束时间"></el-table-column>
      <el-table-column prop="addTime" label="添加时间"></el-table-column>

      <!-- 自定义列 -->
      <el-table-column fixed="right" label="操作" width="120">
        <!-- scope 指整个classList 的数据对象  scope.row 可以去到当前行数据 -->
        <template slot-scope="scope">
          <el-button @click.native.prevent="deleteRow(scope.row)" type="text" size="small">移除</el-button>
        </template>
      </el-table-column>
    </el-table>
    </el-card>
    
    
  </div>
</template>

<script>
import axios from "axios";
export default {
  name: "clazz", // devTool 调试 方便找到组件
  data() {
    return {
      title: "hello,world",
      search: {},
      classList: []
    };
  },
  computed: {},
  created() {
    this.getClassList();
  },
  mounted() {},
  watch: {},
  methods: {
    getClassList() {
      var url = "http://bufantec.com/api/leju/admin/goods/list";
      axios.get(url).then(res => {
        this.classList = res.data.data.list;
        console.log(res);
      });
    },
    deleteRow(row) {
      console.log("row", row);
    }
  },
  components: {}
};
</script>

<style lang="scss" scoped >
    .clazz-main{
        .my-card{
            margin: 30px 30px;
        }
        .search-block{
            // 样式穿透
            .el-input{
                width: 200px;
            }
        }
    }
</style>
