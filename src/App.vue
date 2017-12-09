<template>
  <div id="app">
    <el-row class='search-row'>
      <el-col class='search-label'>
        <div class="grid-content">查询条件</div>
      </el-col>
      <el-col :span="5">
        <el-input size="mini" v-model="searchCondition" placeholder="请输入内容"></el-input>
      </el-col>
      <el-col class="btn-group">
        <el-button type="primary" size="mini" @click="search">查询</el-button>
        <el-button type="default" size="mini" @click="reset" >重置</el-button>
      </el-col>
      <el-col class='search-label'>
        <div class="grid-content">性别</div>
      </el-col>
      <el-col class="search-sex-radio">
        <el-radio-group v-model="sexRadio">
          <el-radio :label="1">全部</el-radio>
          <el-radio :label="2">男</el-radio>
          <el-radio :label="3">女</el-radio>
        </el-radio-group>
      </el-col>
    </el-row>
    <el-row class='search-row'>
      <el-col class='search-label'>
        <div class="grid-content">年龄</div>
      </el-col>
      <el-col class="search-age-radio">
        <el-radio-group v-model="ageRadio">
          <el-radio :label="1">不限</el-radio>
          <el-radio :label="2">0-15岁</el-radio>
          <el-radio :label="3">15-30岁</el-radio>
          <el-radio :label="4">30-40岁</el-radio>
          <el-radio :label="5">40岁以上</el-radio>
          <el-radio :label="6">
            自定义 &nbsp
            <el-input v-model="minAge" size="mini" class='mini-input'></el-input> 至
            <el-input size="mini" class='mini-input' v-model="maxAge"></el-input>
          </el-radio>
        </el-radio-group>
      </el-col>
    </el-row>
    <el-row class='operate-row'>
      <el-col class='btn-group-operate'>
        <el-button type="default" size="mini" @click="add">新增</el-button>
        <el-button type="default" size="mini">复制</el-button>
        <el-button type="default" size="mini">剪切</el-button>
        <el-button type="default" size="mini">批量删除</el-button>
        <el-tag v-show="showTag" closable type="warning" class="operate-warn-tag" @close="showTag=false">
          先选择两个以上目录方可使用
        </el-tag>
      </el-col>
    </el-row>
    <el-table :data="tableData" style="
    width: 100%;
    border: 1px solid #e6ebf5;
    margin-top:20px;" max-height="1000" header-row-class-name="table-header">
      <el-table-column type="selection" width="80">
      </el-table-column>
      <el-table-column fixed prop="name" label="姓名" width="100" align="center">
      </el-table-column>
      <el-table-column prop="avatar" label="头像" min-width="160" align="center">
        <template slot-scope="scope">
          <img class="avatar" :src="scope.row.avatar" />
        </template>
      </el-table-column>
      <el-table-column prop="sex" label="性别" width="80" align="center">
      </el-table-column>
      <el-table-column prop="idnumber" label="身份证号" min-width="200" align="center">
      </el-table-column>
      <el-table-column prop="address" label="所在库" width="100" align="center">
      </el-table-column>
      <el-table-column prop="operate" label="操作" min-width="320" align="center">
        <template slot-scope="scope">
          <span class="operate-span">详情</span> |
          <span class="operate-span">编辑</span> |
          <span class="operate-span">删除</span> |
          <span class="operate-span">添加人像</span>
        </template>
      </el-table-column>
    </el-table>
  </div>
</template>
<script>
export default {
  name: 'app',
  components: {},
  data() {
    return {
      searchCondition: '',
      ageRadio: 1,
      sexRadio: 1,
      minAge: '',
      maxAge: '',
      showTag: true,
      tableData: [{
          name: '张军',
          avatar: 'https://ss1.bdstatic.com/70cFuXSh_Q1YnxGkpoWK1HF6hhy/it/u=3946001806,2014056533&fm=27&gp=0.jpg',
          sex: '男',
          idnumber: '5001233423424234',
          address: '重庆',
        },
        {
          name: '张军1',
          avatar: 'https://ss1.bdstatic.com/70cFuXSh_Q1YnxGkpoWK1HF6hhy/it/u=3946001806,2014056533&fm=27&gp=0.jpg',
          sex: '男',
          idnumber: '5001233423424234',
          address: '重庆',
        }
      ]
    }
  },
  methods:{
    search(){
      console.log(this.ageRadio,this.sexRadio,this.searchCondition)

      //根据 上面这三个参数，去发ajax请求获取数据，把数据按照上面tableData的格式放到this.tableData里，页面就会自动把表格显示出来
    },
    reset(){
      this.ageRadio=1;
      this.sexRadio=1;
      this.searchCondition=''
    },
    add(){
      //增加操作，对应上面的增加按钮
      //其它按钮也像这样添加click事件就可以了  (@click)
    }
  }
}

</script>
<style lang="less" scoped>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

.search-row {
  background-color: #f8f8f8;
  padding: 10px;
  .search-label {
    width: 70px;
  }
  .grid-content {
    font-size: 14px;
    line-height: 30px;
    &:last {
      border-bottom: 1px solid #dedede;
    }
  }
  .btn-group {
    width: 150px;
  }
  .search-sex-radio {
    width: 200px;
    margin-top: 3px;
  }
  .search-age-radio {
    width: 700px;
  }
  .mini-input {
    width: 50px;
  }
}

.operate-row {
  font-size: 14px;
  line-height: 30px;
  text-align: left;
  .btn-group-operate {
    margin-top: 20px;
    margin-left: 15px;
  }
  .operate-warn-tag {
    margin-left: 20px;
  }
}


</style>
<style lang="less">
.table-header {
  background-color: #f6f7f9!important;
}
.avatar{
  width:100px;
}
.operate-span{
  color:blue;
  cursor: pointer;
}
</style>
