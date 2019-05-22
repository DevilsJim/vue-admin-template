<template>
  <div class="app-container my-customer">
    <el-tabs type="border-card" v-model="activeTabsName">
      <el-tab-pane label="全部客户" name="first">
        <el-table
          v-loading="listLoading"
          :data="list"
          element-loading-text="Loading"
          fit
          highlight-current-row
          @selection-change="handleSelectionChange"
        >
          <el-table-column type="selection" width="55"></el-table-column>
          <el-table-column align="center" label="ID" type="index" width="55"></el-table-column>
          <el-table-column prop="date" label="日期" sortable width="180"></el-table-column>
          <el-table-column prop="name" label="姓名" sortable width="180"></el-table-column>
          <el-table-column prop="address" label="地址"></el-table-column>
        </el-table>
      </el-tab-pane>
      <el-tab-pane label="近三天待跟进" name="second">
      </el-tab-pane>
      <el-tab-pane label="近一周待跟进" name="third">
      </el-tab-pane>
      <el-tab-pane label="近一月待跟进" name="fourth">
      </el-tab-pane>
      <el-tab-pane label="超一个月未回访" name="fifth">
      </el-tab-pane>
      <el-tab-pane label="即将掉入公海" name="sixth">
      </el-tab-pane>
      <el-tab-pane label="录入客户" name="seventh">
      </el-tab-pane>
      <el-tab-pane label="成单客户" name="eighth">
        <el-table
          v-loading="listLoading"
          :data="tableData2"
          element-loading-text="Loading"
          fit
          highlight-current-row
          @selection-change="handleSelectionChange"
        >
          <el-table-column type="selection" width="55"></el-table-column>
          <el-table-column align="center" label="ID" type="index" width="55"></el-table-column>
          <el-table-column prop="name" label="客户名称" width="180"></el-table-column>
          <el-table-column label="联系人姓名" width="210" class-name="user-info">
            <template slot-scope="scope">
              <!--{{ scope.row.userInfo }}-->
              <span class="user-name">姓名: {{scope.row.userInfo.userName}}</span>
              <span class="user-phone">电话: {{scope.row.userInfo.phone}}</span>
              <svg-icon icon-class="message" class-name="message" />
              <svg-icon icon-class="phone" class-name="phone" />
            </template>
          </el-table-column>
          <el-table-column prop="tags" label="客户标签"></el-table-column>
          <el-table-column prop="member" label="会员"></el-table-column>
          <el-table-column prop="business" label="意向业务"></el-table-column>
          <el-table-column prop="type" label="客户类型"></el-table-column>
          <el-table-column prop="dynamic" label="最新动态"></el-table-column>
          <el-table-column prop="plannedFollowUpTime" label="计划跟进时间" sortable></el-table-column>
          <el-table-column prop="paymentAmount" label="付费时间" sortable></el-table-column>
          <el-table-column prop="FirstPaymentTime" label="首次付费时间" sortable></el-table-column>
          <el-table-column prop="FinalPaymentTime" label="最后付费时间" sortable></el-table-column>
          <el-table-column label="操作"></el-table-column>
        </el-table>
      </el-tab-pane>
    </el-tabs>
  </div>
</template>

<script>
// import { getList } from '@/api/table'

export default {
  name: 'Icons',
  data() {
    return {
      list: null,
      listLoading: true,
      activeTabsName: 'eighth',
      tableData: [
        {
          date: '2016-05-02',
          name: '王小虎',
          address: '上海市普陀区金沙江路 1518 弄'
        },
        {
          date: '2016-05-04',
          name: '王小虎',
          address: '上海市普陀区金沙江路 1517 弄'
        },
        {
          date: '2016-05-01',
          name: '王小虎',
          address: '上海市普陀区金沙江路 1519 弄'
        }
      ],
      tableData2: [
        {
          name: '北京知果果科技有限公司',
          userInfo: { userName: '张三', phone: 1334534567 },
          tags: ['已成单', '新客户', '高价值'],
          member: '青苹果会员', // 0:普通用户， 1：青苹果会员， 2：红苹果会员
          business: '商标注册',
          type: '企业用户',
          dynamic: '黑天天：捡入私海 2019-03-01 14:32:35',
          plannedFollowUpTime: '2018-12-28',
          paymentAmount: 1600.00,
          FirstPaymentTime: '2018-09-18 15:00:30',
          FinalPaymentTime: '2019-05-20 00:00:00'
        }
      ]
    }
  },
  created() {
    this.fetchData()
  },
  methods: {
    handleSelectionChange(val) {
      console.log(val)
    },
    fetchData() {
      this.listLoading = true
      if (this.tableData) {
        this.list = this.tableData
        this.listLoading = false
      }
      // getList().then(response => {
      //   this.list = response.data.items
      //   this.listLoading = false
      // })
    }
  }
}
</script>
<style lang="scss" scoped>
.my-customer{
  .user-info{
    .user-name{
      display: block;
    }
    .user-phone{
      display: inline-block;
    }
    .message, .phone{
      cursor: pointer;
      display: inline-block;
      font-size: 20px;
      margin-left: 5px;
    }
  }
}
</style>
