<template>
  <div class="app-container my-customer">
    <el-tabs type="border-card" v-model="activeTabsName">
      <el-tab-pane label="全部客户" name="first">
        <el-table
          v-loading="listLoading"
          :data="list"
          element-loading-text="Loading"
          fit
          border
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
        <!--Form-->
        <el-form :inline="true" :model="formInline">
          <!-- 选择搜索条件 -->
          <el-form-item>
            <el-select v-model="formInline.region" clearable placeholder="请选择搜索条件">
              <el-option label="公司名称" value="companyName"></el-option>
              <el-option label="联系人手机号" value="latentUserMobile"></el-option>
              <el-option label="联系人座机号" value="latentTelephone"></el-option>
              <el-option label="联系人姓名" value="latentNickName"></el-option>
              <el-option label="用户ID" value="latentUserId"></el-option>
            </el-select>
          </el-form-item>
          <!-- 输对应搜索条件的内容 -->
          <el-form-item>
            <el-input v-model="formInline.user" placeholder="请输入搜索内容"></el-input>
          </el-form-item>
          <!-- 下次跟进时间 -->
          <el-form-item>
            <el-date-picker
              v-model="value1"
              type="daterange"
              range-separator="至"
              start-placeholder="计划下次开始跟进时间"
              end-placeholder="计划下次结束跟进时间"
              format="yyyy-MM-dd HH-mm-ss"
              value-format="yyyy-MM-dd HH-mm-ss"
              :default-time="['00:00:00', '23:59:59']">
            </el-date-picker>
            <!--<div class="demonstration">值：{{ value1 }}</div>-->
          </el-form-item>
          <!-- 跟进时间 -->
          <el-form-item>
            <el-date-picker
              v-model="value2"
              type="daterange"
              range-separator="至"
              start-placeholder="开始跟进时间"
              end-placeholder="结束跟进时间"
              format="yyyy-MM-dd HH-mm-ss"
              value-format="yyyy-MM-dd HH-mm-ss"
              :default-time="['00:00:00', '23:59:59']">
            </el-date-picker>
            <!--<div class="demonstration">值：{{ value2 }}</div>-->
          </el-form-item>
          <!-- 产品类型 -->
          <el-form-item>
            <el-select v-model="formInline.region1" clearable placeholder="请选择产品类型">
              <el-option label="接口返回数据" value="productType"></el-option>
            </el-select>
          </el-form-item>
          <!-- 产品小类 -->
          <el-form-item>
            <el-select v-model="formInline.region2" clearable placeholder="请选择产品小类">
              <el-option label="接口返回数据" value="productSubcategory"></el-option>
            </el-select>
          </el-form-item>
          <!-- 客户标签 -->
          <el-form-item>
            <el-select v-model="formInline.region3" clearable placeholder="请选择客户标签">
              <el-option label="新客户" value="newCustomer"></el-option>
              <el-option label="渠道客户" value="channelCustomer"></el-option>
            </el-select>
          </el-form-item>
          <!-- 意向度 -->
          <el-form-item>
            <el-select v-model="formInline.region4" clearable placeholder="请选择意向度">
              <el-option label="无意向" value="1"></el-option>
              <el-option label="有意向" value="2"></el-option>
              <el-option label="高意向" value="3"></el-option>
            </el-select>
          </el-form-item>
          <!-- 客户价值 -->
          <el-form-item>
            <el-select v-model="formInline.region4" clearable placeholder="请选择客户价值">
              <el-option label="高价值" value="1"></el-option>
              <el-option label="中价值" value="2"></el-option>
              <el-option label="低价值" value="3"></el-option>
            </el-select>
          </el-form-item>
          <!-- 公司所在地 -->
          <el-form-item>
            <el-input v-model="formInline.user1" placeholder="请输入公司所在地"></el-input>
          </el-form-item>
          <!-- 查询公司范围 -->
          <el-form-item>
            <el-select v-model="formInline.region5" clearable placeholder="请选择查询公司范围">
              <el-option label="全部公司" value="1"></el-option>
              <el-option label="主显公司" value="1"></el-option>
              <el-option label="从显公司" value="2"></el-option>
            </el-select>
          </el-form-item>
          <!-- 操作 -->
          <el-form-item>
            <el-button type="primary" @click="onSubmit">搜索</el-button>
            <el-button type="primary" @click="onSubmit">重置</el-button>
            <el-button type="success" @click="onSubmit">创建客户</el-button>
          </el-form-item>
        </el-form>
        <!-- Table -->
        <el-table
          v-loading="listLoading"
          :data="tableData2"
          element-loading-text="Loading"
          fit
          border
          highlight-current-row
          @selection-change="handleSelectionChange"
        >
          <el-table-column type="selection" width="55" align="center"></el-table-column>
          <el-table-column label="序号" type="index" width="60" align="center"></el-table-column>
          <el-table-column label="客户名称" width="210" class-name="name" header-align="center">
            <template slot-scope="scope">
              <span>{{scope.row.name}}</span>
              <el-tooltip placement="top">
                <div slot="content">
                  <!--{{ generateElementIconCode(item) }}-->
                  后台返回数据
                </div>
                <svg-icon icon-class="message" class-name="message" />
              </el-tooltip>
            </template>
          </el-table-column>
          <el-table-column label="联系人姓名" width="190" class-name="user-info" header-align="center">
            <template slot-scope="scope">
              <span class="user-name">姓名: {{scope.row.userInfo.userName}}</span>
              <span class="user-phone">电话: {{scope.row.userInfo.phone}}</span>
              <el-tooltip placement="top" content="点击发送短信" >
                <svg-icon icon-class="mail" class-name="mail" />
              </el-tooltip>
              <el-tooltip placement="top" content="点击拨打电话" >
                <svg-icon icon-class="phone" class-name="phone" />
              </el-tooltip>
            </template>
          </el-table-column>
          <el-table-column label="客户标签" width="215" class-name="tags" header-align="center">
            <template slot-scope="scope">
              <el-tag v-for="item in scope.row.tags" :key="item">{{item}}</el-tag>
            </template>
          </el-table-column>
          <el-table-column prop="member" label="会员" width="100" align="center"></el-table-column>
          <el-table-column prop="business" label="意向业务" width="100" align="center"></el-table-column>
          <el-table-column prop="type" label="客户类型" width="100" align="center"></el-table-column>
          <el-table-column label="最新动态">
            <template slot-scope="scope">
              <span v-html="scope.row.dynamic"></span>
            </template>
          </el-table-column>
          <el-table-column prop="plannedFollowUpTime" label="计划跟进时间" sortable width="130" align="center"></el-table-column>
          <el-table-column prop="paymentAmount" label="付费金额" sortable width="120" align="center"></el-table-column>
          <el-table-column prop="FirstPaymentTime" label="首次付费时间" sortable width="130" align="center"></el-table-column>
          <el-table-column prop="FinalPaymentTime" label="最后付费时间" sortable width="130" align="center"></el-table-column>
          <el-table-column label="操作" align="center" class-name="operation" fixed="right" width="190">
            <el-button type="primary" size="small">跟进</el-button>
            <el-button type="primary" size="small">待客下单</el-button>
          </el-table-column>
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
      formInline: {
        user: '',
        region: ''
      },
      value1: '',
      value2: '',
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
          member: '普通用户', // 0:普通用户， 1：青苹果会员， 2：红苹果会员
          business: '专利',
          type: '企业用户',
          dynamic: '黑天天：分配的客户 2019-03-01 14:32:35',
          plannedFollowUpTime: '2018-12-28',
          paymentAmount: '1600.00',
          FirstPaymentTime: '2018-09-18',
          FinalPaymentTime: '2019-05-20'
        },
        {
          name: '北京知果果科技有限公司',
          userInfo: { userName: '张三', phone: 1334534567 },
          tags: ['已成单', '高价值'],
          member: '青苹果会员', // 0:普通用户， 1：青苹果会员， 2：红苹果会员
          business: '版权',
          type: '渠道用户',
          dynamic: '黑天天：捡入私海 2019-03-01 14:32:35',
          plannedFollowUpTime: '2018-12-28',
          paymentAmount: '1600.00',
          FirstPaymentTime: '2018-09-18',
          FinalPaymentTime: '2019-05-20'
        },
        {
          name: '北京知果果科技有限公司',
          userInfo: { userName: '张三', phone: 1334534567 },
          tags: ['高价值'],
          member: '红苹果会员', // 0:普通用户， 1：青苹果会员， 2：红苹果会员
          business: '商标',
          type: '个体',
          dynamic: '黑天天：释放到公海 2019-03-01 14:32:35',
          plannedFollowUpTime: '2018-12-28',
          paymentAmount: '1600.00',
          FirstPaymentTime: '2018-09-18',
          FinalPaymentTime: '2019-05-20'
        }
      ]
    }
  },
  created() {
    this.fetchData()
  },
  methods: {
    onSubmit() {
      this.$message('submit!')
    },
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
  .el-form{
    .el-date-editor {
      width: 410px;
      /deep/ .el-range-input{
        width: 80%;
      }
      /deep/ .el-range-separator{  // 加 /deep/ 或 >>> 是为了给 element 元素添加自定义样式
        padding: 0;
      }
    }
    .el-button{
      padding: 11px 15px;
      margin-left: 20px;
      &:first-child{
        margin-left: 10px;
      }
      &:last-child{
        margin-left: 40px;
      }
      /deep/ span{
        font-size: 16px;
      }
    }
  }
  .el-table{
    .svg-icon{
      cursor: pointer;
      display: inline-block;
      font-size: 18px;
    }
    .name{
      span{
        display: inline-block;
        overflow:hidden;
        text-overflow:ellipsis;
        white-space:nowrap;
        width: 160px;
        vertical-align: top;
      }
    }
    .user-info{
      .user-name{
        display: block;
      }
      .user-phone{
        display: inline-block;
      }
      .svg-icon{
        margin-left: 5px;
      }
    }
    .tags{
      .el-tag{
        margin-right: 5px;
        font-size: 14px;
        height: 30px;
        line-height: 28px;
        padding: 0 8px;
      }
      .el-tag:last-child{
        margin-right: 0;
      }
    }
    .operation{
      .el-button{
        font-size: 14px;
      }
    }
  }
}
</style>
