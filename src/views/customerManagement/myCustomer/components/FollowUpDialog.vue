<template>
  <el-dialog title="跟进" :visible.sync="visible" width="650px">
    <el-form ref="dataForm" :model="temp" label-width="120px">
      <!-- 客户类型 -->
      <el-form-item label="跟进联系人:">
        <el-input v-model="temp.user" placeholder="请输入跟进联系人" clearable></el-input>
      </el-form-item>

      <!-- 跟进方式 -->
      <el-form-item label="跟进方式:">
        <el-radio-group v-model="temp.radio2">
          <el-radio-button label="上海"></el-radio-button>
          <el-radio-button label="北京"></el-radio-button>
          <el-radio-button label="广州"></el-radio-button>
          <el-radio-button label="深圳"></el-radio-button>
        </el-radio-group>
      </el-form-item>

      <!-- 是否联系 -->
      <el-form-item label="是否联系:">
        <el-radio v-model="temp.radio1" label="1">已联系上</el-radio>
        <el-radio v-model="temp.radio1" label="2">未联系上</el-radio>
      </el-form-item>

      <!-- 意向度 -->
      <el-form-item label="意向度:">
        <el-select v-model="temp.region4" clearable placeholder="请选择意向度">
          <el-option label="无意向" value="1"></el-option>
          <el-option label="有意向" value="2"></el-option>
          <el-option label="高意向" value="3"></el-option>
        </el-select>
      </el-form-item>

      <!-- 意向业务 -->
      <el-form-item label="意向业务:">
        <div class="block">
          <el-cascader
            clearable
            expand-trigger="hover"
            :options="options"
            v-model="temp.selectedOptions"
            @change="handleChange">
          </el-cascader>
        </div>
      </el-form-item>

      <!-- 下次跟进时间 -->
      <el-form-item label="下次跟进时间:">
        <el-date-picker
          v-model="temp.value1"
          type="daterange"
          range-separator="至"
          start-placeholder="计划下次开始跟进时间"
          end-placeholder="计划下次结束跟进时间"
          format="yyyy-MM-dd HH-mm-ss"
          value-format="yyyy-MM-dd HH-mm-ss"
          :default-time="['00:00:00', '23:59:59']">
        </el-date-picker>
      </el-form-item>

      <!-- 跟进备注 -->
      <el-form-item label="备注:">
        <el-input type="textarea" v-model="temp.desc" placeholder="请输入内容"></el-input>
      </el-form-item>

      <!-- 客户价值 -->
      <el-form-item label="客户价值:">
        <el-radio-group v-model="temp.radio2">
          <el-radio-button label="未标记"></el-radio-button>
          <el-radio-button label="低价值"></el-radio-button>
          <el-radio-button label="中价值"></el-radio-button>
          <el-radio-button label="高价值"></el-radio-button>
        </el-radio-group>
      </el-form-item>

      <!-- 上传文件 -->
      <el-form-item label="上传文件:">
        <el-upload
          action="https://jsonplaceholder.typicode.com/posts/"
          list-type="picture-card"
          :on-preview="handlePictureCardPreview"
          :on-remove="handleRemove">
          <i class="el-icon-plus"></i>
        </el-upload>
        <el-dialog :visible.sync="dialogVisible">
          <img width="100%" :src="dialogImageUrl" alt="">
        </el-dialog>
      </el-form-item>

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
  name: 'FollowUpDialog',
  props: {
    visible: {
      type: Boolean,
      default: false
    }
  },
  data() {
    return {
      temp: {},
      options: [
        {
          value: 'zhinan',
          label: '指南',
          children: [
            {
              value: 'shejiyuanze',
              label: '设计原则'
            }
          ]
        },
        {
          value: 'zujian',
          label: '组件',
          children: [
            {
              value: 'basic',
              label: 'Basic'
            }
          ]
        }
      ],
      selectedOptions: [],
      dialogImageUrl: '',
      dialogVisible: false
    }
  },
  methods: {
    handleChange(val) {
      console.log(val)
    },
    handleRemove(file, fileList) {
      console.log(file, fileList)
    },
    handlePictureCardPreview(file) {
      this.dialogImageUrl = file.url
      this.dialogVisible = true
    }
  }
}
</script>

<style scoped>
/deep/ .el-dialog .el-dialog__header{
  border-bottom: 1px solid #ddd;
  padding-bottom: 20px;
}
/deep/ .el-dialog .el-dialog__body{
  padding:30px 80px 0 50px
}
/deep/ .el-form .el-form-item__label, /deep/ .el-form .el-form-item__content, /deep/ .el-form .el-radio{
  font-weight: normal;
  font-size: 15px;
}
/deep/ .el-form .el-form-item__content .el-select {
  width: 100%;
}
.el-date-editor {
  width: 400px;
}
.el-cascader{
  width: 100%;
}
/deep/ .el-date-editor .el-range-input{
  width: 80%;
}
</style>
