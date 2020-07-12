<template>
  <div>
    <el-row :gutter="15">
      <el-col :span="12"><div class="grid-content bg-purple">
        <el-form ref="queryForm" :model="queryParams" :inline="true">
          <el-form-item label="证件号码" prop="applicationNo">
            <el-input
              v-model="queryParams.applicationNo"
              placeholder="请输入证件号码"
              clearable
              size="small"
              @keyup.enter.native="handleQuery"
            />
          </el-form-item>

          <el-form-item label="姓名" prop="userName">
            <el-input
              v-model="queryParams.userName"
              placeholder="请输入姓名"
              clearable
              size="small"
              maxlength:200
              @keyup.enter.native="handleQuery"
            />
          </el-form-item>
          <el-form-item label="通道" prop="port">
            <el-select v-model="queryParams.port" size="small" placeholder="请选择通道" clearable :style="{width: '100%'}" style="width: 200px">
              <el-option
                v-for="(item, index) in portOptions"
                :key="index"
                :label="item.label"
                :value="item.value"
                :disabled="item.disabled"
              />
            </el-select>
          </el-form-item>
          <el-form-item label="通关日期">
            <el-col :span="11">
              <el-date-picker v-model="queryParams.applyDate" type="date" placeholder="选择开始日期" size="small" style="width: 100%;" />
            </el-col>
            <el-col class="line" :span="1">至</el-col>
            <el-col :span="11">
              <el-date-picker v-model="queryParams.endDate" placeholder="选择结束时间" size="small" style="width: 100%;" />
            </el-col>
          </el-form-item>
          <el-form-item>
            <el-button type="primary" icon="el-icon-search" size="mini" @click="handleQuery">查询</el-button>
            <el-button type="primary" size="mini" @click="handleQuery">扫描二维码</el-button>
            <el-button icon="el-icon-end" size="mini" @click="resetQuery">结束流程</el-button>
          </el-form-item>
        </el-form>

        <el-table
          :data="tableData"
          style="width: 100%"
          :row-class-name="tableRowClassName"
          @row-click="handlerRow"
        >
          <el-table-column
            prop="num"
            label="序号"
            width="40"
          />
          <el-table-column
            prop="name"
            label="姓名"
            width="100"
          />
          <el-table-column
            prop="sex"
            label="性别"
            width="40"
          >
          </el-table-column>
          <el-table-column
            prop="country"
            label="国籍"
          />
          <el-table-column
            prop="zjhm"
            label="证件号码"
          />
          <el-table-column
            prop="port"
            label="口岸通道"
          />
          <el-table-column
            prop="outOrIn"
            label="出入境"
          />
          <el-table-column
            prop="passTime"
            label="通关时间"
          />
        </el-table>
      </div>
      </el-col>
      <el-col :span="12">
        <el-form ref="elForm" :model="formData" :rules="rules" size="medium" label-width="100px">
          <el-card class="box-card">
            <div slot="header" class="clearfix">
              <span>口岸新型冠状病毒感染的肺炎染疫人/染疫嫌疑人转交记录单</span>
            </div>
          <el-col :span="12">
            <el-form-item label="交通工具/航班号" prop="field101">
              <el-input
                v-model="formData.field101"
                placeholder="请输入交通工具/航班号"
                clearable
                :style="{width: '100%'}"
              />
            </el-form-item>
          </el-col>
          <el-col :span="12">
            <el-form-item label="入境日期" prop="field102">
              <el-date-picker
                v-model="formData.field102"
                format="yyyy-MM-dd"
                value-format="yyyy-MM-dd"
                :style="{width: '100%'}"
                placeholder="请选择入境日期"
                clearable
              />
            </el-form-item>
          </el-col>
          <el-col :span="12">
            <el-form-item label="检疫医师" prop="field103">
              <el-input v-model="formData.field103" placeholder="检疫医师签字" clearable :style="{width: '100%'}" />
            </el-form-item>
          </el-col>
          <el-col :span="12">
            <el-form-item label="医师电话" prop="field104">
              <el-input v-model="formData.field104" placeholder="医师电话" clearable :style="{width: '100%'}" />
            </el-form-item>
          </el-col>
          <el-col :span="12">
            <el-form-item label="救护车号" prop="field105">
              <el-input v-model="formData.field105" placeholder="请输入救护车号" clearable :style="{width: '100%'}" />
            </el-form-item>
          </el-col>
          <el-col :span="12">
            <el-form-item label="离开时间" prop="field106">
              <el-date-picker
                v-model="formData.field106"
                format="yyyy-MM-dd"
                value-format="yyyy-MM-dd"
                :style="{width: '100%'}"
                placeholder="请选择离开时间"
                clearable
              />
            </el-form-item>
          </el-col>
          <el-col :span="12">
            <el-form-item label="拟送医院" prop="field107">
              <el-input v-model="formData.field107" placeholder="请输入拟送医院" clearable :style="{width: '100%'}" />
            </el-form-item>
          </el-col>
          <el-col :span="12">
            <el-form-item label="救护车医师" prop="field108">
              <el-input v-model="formData.field108" placeholder="救护车医师签字" clearable :style="{width: '100%'}" />
            </el-form-item>
          </el-col>
          <el-col :span="12">
            <el-form-item label="救护车医师电话" prop="field109">
              <el-input
                v-model="formData.field109"
                placeholder="请输入电话救护车医师电话"
                clearable
                :style="{width: '100%'}"
              />
            </el-form-item>
          </el-col>
          <el-col :span="12">
            <el-form-item label="接受医院" prop="field110">
              <el-input v-model="formData.field110" placeholder="请输入接受医院" clearable :style="{width: '100%'}" />
            </el-form-item>
          </el-col>
          <el-col :span="12">
            <el-form-item label="接诊医生" prop="field111">
              <el-input v-model="formData.field111" placeholder="接诊医生签字" clearable :style="{width: '100%'}" />
            </el-form-item>
          </el-col>
          <el-col :span="23">
            <el-form-item label="诊断结果及处理意见" prop="field112">
              <el-input
                v-model="formData.field112"
                type="textarea"
                placeholder="请输入诊断结果及处理意见"
                :autosize="{minRows: 4, maxRows: 4}"
                :style="{width: '100%'}"
              />
            </el-form-item>
          </el-col>
          <el-col :span="12">
            <el-form-item label="主检医师" prop="field113">
              <el-input v-model="formData.field113" placeholder="主检医师签字" clearable :style="{width: '100%'}" />
            </el-form-item>
          </el-col>
          <el-col :span="12">
            <el-form-item label="主检医师电话" prop="field114">
              <el-input v-model="formData.field114" placeholder="主检医师电话" clearable :style="{width: '100%'}" />
            </el-form-item>
          </el-col>
          <el-col :span="12">
            <el-form-item label="日期" prop="field115">
              <el-date-picker
                v-model="formData.field115"
                format="yyyy-MM-dd"
                value-format="yyyy-MM-dd"
                :style="{width: '100%'}"
                placeholder="请选择日期"
                clearable
              />
            </el-form-item>
          </el-col>
          <el-col>
            <template><font color="#ff0000">注：请病人接收医院做出诊断及处理意见后立即将此单传真至海关部门，以便做好疫情后续管理工作。
            </font></template>
          </el-col>
          <el-col :span="12">
            <el-form-item label="传真号码" prop="field116">
              <el-input v-model="formData.field116" placeholder="传真号码" clearable :style="{width: '100%'}" />
            </el-form-item>
          </el-col>
          <el-col :span="12">
            <el-form-item label="联系电话" prop="field117">
              <el-input v-model="formData.field117" placeholder="联系电话" clearable :style="{width: '100%'}" />
            </el-form-item>
          </el-col>

          <el-col>
            <template>
              <p style="color: #606266">              本转诊单一式两联，一份由海关保存，另一联请救护车医师交给接收医院接诊医师
              </p>
            </template>
          </el-col>
            <el-col :span="24">
              <el-form-item size="large">
                <el-button type="primary" size="mini" @click="submitForm">提交</el-button>
                <el-button @click="resetForm" size="mini">重置</el-button>
              </el-form-item>
            </el-col>
          </el-card>
        </el-form>
      </el-col>
    </el-row>
  </div>
</template>
<script>
export default {
  components: {},
  props: [],
  data() {
    return {
      tableData: [{
        num: '1',
        name: '王小虎',
        sex: '男',
        country: '中国',
        zjhm: '10012231312131',
        port: 'xxx口岸xx通道',
        outOrIn: '入境',
        passTime: '2020-07-10 22:22'
      }, {
        num: '2',
        name: '张晓丽',
        sex: '女',
        country: '中国',
        zjhm: '10012231312131',
        port: 'xxx口岸xx通道',
        outOrIn: '入境',
        passTime: '2020-07-10 22:22'
      }, {
        num: '3',
        name: '王小',
        sex: '男',
        country: '中国',
        zjhm: '10012231312131',
        port: 'xxx口岸xx通道',
        outOrIn: '入境',
        passTime: '2020-07-10 22:22'
      }, {
        num: '4',
        name: '王虎',
        sex: '男',
        country: '中国',
        zjhm: '10012231312131',
        port: 'xxx口岸xx通道',
        outOrIn: '入境',
        passTime: '2020-07-10 22:22'
      }],

      queryParams: {
        pageNum: 1,
        pageSize: 10,
        applicationNo: undefined,
        userId: undefined,
        userName: undefined,
        clientName: undefined,
        clientCode: undefined,
        passType: undefined,
        type: undefined,
        customsNo: undefined,
        containerNo: undefined,
        carNo: undefined,
        applyDate: undefined,
        endDate: undefined,
        status: undefined,
        port: undefined
      },
      formData: {
        field101: undefined,
        field102: null,
        field103: undefined,
        field104: undefined,
        field105: undefined,
        field106: null,
        field107: undefined,
        field108: undefined,
        field109: undefined,
        field110: undefined,
        field111: undefined,
        field112: undefined,
        field113: undefined,
        field114: undefined,
        field115: null,
        field116: undefined,
        field117: undefined
      },
      rules: {
        field101: [{
          required: true,
          message: '请输入交通工具/航班号',
          trigger: 'blur'
        }],
        field102: [{
          required: true,
          message: '请选择入境日期',
          trigger: 'change'
        }],
        field103: [{
          required: true,
          message: '检疫医师签字',
          trigger: 'blur'
        }],
        field104: [{
          required: true,
          message: '医师电话',
          trigger: 'blur'
        }],
        field105: [{
          required: true,
          message: '请输入救护车号',
          trigger: 'blur'
        }],
        field106: [{
          required: true,
          message: '请选择离开时间',
          trigger: 'change'
        }],
        field107: [{
          required: true,
          message: '请输入拟送医院',
          trigger: 'blur'
        }],
        field108: [{
          required: true,
          message: '救护车医师签字',
          trigger: 'blur'
        }],
        field109: [{
          required: true,
          message: '请输入电话救护车医师电话',
          trigger: 'blur'
        }],
        field110: [{
          required: true,
          message: '请输入接受医院',
          trigger: 'blur'
        }],
        field111: [{
          required: true,
          message: '接诊医生签字',
          trigger: 'blur'
        }],
        field112: [{
          required: true,
          message: '请输入诊断结果及处理意见',
          trigger: 'blur'
        }],
        field113: [{
          required: true,
          message: '主检医师签字',
          trigger: 'blur'
        }],
        field114: [{
          required: true,
          message: '主检医师电话',
          trigger: 'blur'
        }],
        field115: [{
          required: true,
          message: '请选择日期',
          trigger: 'change'
        }],
        field116: [{
          required: true,
          message: '传真号码',
          trigger: 'blur'
        }],
        field117: [{
          required: true,
          message: '联系电话',
          trigger: 'blur'
        }]
      }
    }
  },
  computed: {},
  watch: {},
  created() {},
  mounted() {},
  methods: {
    submitForm() {
      this.$refs['elForm'].validate(valid => {
        if (!valid) return
        // TODO 提交表单
      })
    },
    resetForm() {
      this.$refs['elForm'].resetFields()
    }
  }
}

</script>
<style>
</style>
