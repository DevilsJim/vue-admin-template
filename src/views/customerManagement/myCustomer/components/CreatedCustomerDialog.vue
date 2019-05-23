<template>
  <el-dialog title="新增客户" :visible.sync="visible" width="650px">
    <el-form ref="dataForm" :rules="rules" :model="temp" label-width="75px" size="medium">
      <!-- 客户类型 -->
      <el-form-item label="客户类型" prop="customerType" class="label-style" label-width="80px">
        <el-radio-group v-model="temp.radio">
          <el-radio :label="3">企业用户</el-radio>
          <el-radio :label="6">个体工商</el-radio>
          <el-radio :label="9">自然人</el-radio>
        </el-radio-group>
      </el-form-item>

      <!-- 客户信息 -->
      <el-form-item label="客户信息" class="label-style" label-width="80px"></el-form-item>
      <!-- 公司名称, 意向业务 -->
      <el-row>
        <el-col :span="12" style="padding-right: 15px;">
          <el-form-item label="公司名称:">
            <el-input v-model="temp.user" placeholder="请输入公司名称"></el-input>
          </el-form-item>
        </el-col>
        <el-col :span="12" style="padding-left: 15px;">
          <el-form-item label="意向业务:">
            <el-select v-model="temp.region4" clearable placeholder="请选择意向业务">
              <el-option label="商标服务" value="1"></el-option>
              <el-option label="商标服务" value="2"></el-option>
              <el-option label="商标服务" value="3"></el-option>
            </el-select>
          </el-form-item>
        </el-col>
      </el-row>
      <!-- 行业领域, 人员规模 -->
      <el-row>
        <el-col :span="12" style="padding-right: 15px;">
          <el-form-item label="行业领域:">
            <el-input v-model="temp.user" placeholder="请输入行业领域"></el-input>
          </el-form-item>
        </el-col>
        <el-col :span="12" style="padding-left: 15px;">
          <el-form-item label="人员规模:">
            <el-input v-model="temp.user" placeholder="请输入人员规模"></el-input>
          </el-form-item>
        </el-col>
      </el-row>
      <!-- 地址, 线索来源 -->
      <el-row>
        <el-col :span="12" style="padding-right: 15px;">
          <el-form-item label="地址:">
            <el-input v-model="temp.user" placeholder="请输入地址"></el-input>
          </el-form-item>
        </el-col>
        <el-col :span="12" style="padding-left: 15px;">
          <el-form-item label="线索来源:">
            <el-select v-model="temp.region4" clearable placeholder="请选择线索来源">
              <el-option label="商标服务" value="1"></el-option>
              <el-option label="商标服务" value="2"></el-option>
              <el-option label="商标服务" value="3"></el-option>
            </el-select>
          </el-form-item>
        </el-col>
      </el-row>
      <!-- 渠道用户, 客户星级 -->
      <el-row>
        <el-col :span="12" style="padding-right: 15px;">
          <el-form-item label="渠道用户:">
            <el-radio-group v-model="temp.radio">
              <el-radio :label="1">是</el-radio>
              <el-radio :label="0">否</el-radio>
            </el-radio-group>
          </el-form-item>
        </el-col>
        <el-col :span="12" style="padding-left: 15px;">
          <el-form-item label="客户星级:">
            <el-select v-model="temp.region4" clearable placeholder="请选择客户星级">
              <el-option label="商标服务" value="1"></el-option>
              <el-option label="商标服务" value="2"></el-option>
              <el-option label="商标服务" value="3"></el-option>
            </el-select>
          </el-form-item></el-col>
      </el-row>
      <!-- 备注 -->
      <el-row>
        <el-col :span="24">
          <el-form-item label="备注:">
            <el-input type="textarea" v-model="temp.desc" placeholder="请输入内容"></el-input>
          </el-form-item>
        </el-col>
      </el-row>

      <!-- 联系人信息 -->
      <el-form-item label="联系人信息" class="label-style" label-width="100px"></el-form-item>
      <!-- 姓名, 手机 -->
      <el-row>
        <el-col :span="12" style="padding-right: 15px;">
          <el-form-item label="姓名:">
            <el-input v-model="temp.user" placeholder="请输入客户姓名"></el-input>
          </el-form-item>
        </el-col>
        <el-col :span="12" style="padding-left: 15px;">
          <el-form-item label="手机:">
            <el-input v-model="temp.user" placeholder="请输入手机号"></el-input>
          </el-form-item>
        </el-col>
      </el-row>
      <!-- 职务, 座机 -->
      <el-row>
        <el-col :span="12" style="padding-right: 15px;">
          <el-form-item label="职务:">
            <el-input v-model="temp.user" placeholder="请输入职务"></el-input>
          </el-form-item>
        </el-col>
        <el-col :span="12" style="padding-left: 15px;">
          <el-form-item label="座机:">
            <el-input v-model="temp.user" placeholder="请输入座机号"></el-input>
          </el-form-item>
        </el-col>
      </el-row>
      <!-- 微信, 邮箱 -->
      <el-row>
        <el-col :span="12" style="padding-right: 15px;">
          <el-form-item label="微信:">
            <el-input v-model="temp.user" placeholder="请输入微信号"></el-input>
          </el-form-item>
        </el-col>
        <el-col :span="12" style="padding-left: 15px;">
          <el-form-item label="邮箱:">
            <el-input v-model="temp.user" placeholder="请输入邮箱地址"></el-input>
          </el-form-item>
        </el-col>
      </el-row>
      <!-- QQ -->
      <el-row>
        <el-col :span="12" style="padding-right: 15px;">
          <el-form-item label="QQ:">
            <el-input v-model="temp.user" placeholder="请输入邮箱地址"></el-input>
          </el-form-item>
        </el-col>
      </el-row>

      <!-- 经营情况 -->
      <el-form-item label="经营情况" class="label-style" label-width="80px"></el-form-item>
      <!-- 商标数量, 专利数量 -->
      <el-row>
        <el-col :span="12" style="padding-right: 15px;">
          <el-form-item label="商标数量:">
            <el-input v-model="temp.user" placeholder="请输入商标数量"></el-input>
          </el-form-item>
        </el-col>
        <el-col :span="12" style="padding-left: 15px;">
          <el-form-item label="专利数量:">
            <el-input v-model="temp.user" placeholder="请输入专利数量"></el-input>
          </el-form-item>
        </el-col>
      </el-row>
      <!-- 软著数量, 其他资质 -->
      <el-row>
        <el-col :span="12" style="padding-right: 15px;">
          <el-form-item label="软著数量:">
            <el-input v-model="temp.user" placeholder="请输入软著数量"></el-input>
          </el-form-item>
        </el-col>
        <el-col :span="12" style="padding-left: 15px;">
          <el-form-item label="其他资质:">
            <el-input v-model="temp.user" placeholder="请输入其他资质"></el-input>
          </el-form-item>
        </el-col>
      </el-row>
      <!-- 融资情况 -->
      <el-row>
        <el-col :span="12" style="padding-right: 15px;">
          <el-form-item label="融资情况:">
            <el-input v-model="temp.user" placeholder="请输入融资情况"></el-input>
          </el-form-item>
        </el-col>
      </el-row>
    </el-form>
    <!-- 保存, 取消 -->
    <div slot="footer" class="dialog-footer">
      <el-button @click="createdDialogVisible = false">取消</el-button>
      <el-button type="primary" @click="dialogStatus==='create'?createData():updateData()">保存</el-button>
    </div>
  </el-dialog>
</template>

<script>
export default {
  name: 'CreateCustomerDialog',
  props: {
    visible: {
      type: Boolean,
      default: false
    }
  },
  data() {
    return {
      rules: {},
      temp: {}
    }
  }
}
</script>

<style scoped>
.el-row{
  padding: 0 20px;
}
/deep/ .el-dialog .el-dialog__header{
  border-bottom: 1px solid #ddd;
  padding-bottom: 20px;
}
/deep/ .el-form .el-form-item__label, /deep/ .el-form .el-form-item__content, /deep/ .el-form .el-radio{
  font-weight: normal;
}
/deep/ .el-form .label-style .el-form-item__label{
  font-size: 16px;
  font-weight: bold;
}
/deep/ .el-form .label-style .el-form-item__content{
  margin-top: 30px;
}
</style>
