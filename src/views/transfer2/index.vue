<template>
  <div>
    <el-row :gutter="15">

      <el-col :span="24">
        <el-form ref="elForm" :model="formData" :rules="rules" size="medium" label-width="100px">
          <el-card class="box-card">
            <div slot="header" class="clearfix">
              <span>新冠肺炎疫情防控重点人群移交记录单</span>
            </div>
            <el-row :gutter="20">
              <el-col :span="6" style="width: 300px">
                <el-form-item label="姓名" prop="field127" label-width="100px">
                  <el-input
                    v-model="formData.field127"
                    placeholder="请输入姓名"
                    show-word-limit
                    clearable
                    :style="{width: '100%'}"
                  />
                </el-form-item>
              </el-col>
              <el-col :span="6" style="width: 300px">
                <el-form-item label="性别" prop="field128" lable-width="100px">
                  <el-select v-model="formData.field128" placeholder="请选择性别" clearable :style="{width: '80%'}">
                    <el-option
                      v-for="(item, index) in field128Options"
                      :key="index"
                      :label="item.label"
                      :value="item.value"
                      :disabled="item.disabled"
                    />
                  </el-select>
                </el-form-item>
              </el-col>
              <el-col :span="16" style="width: 300px;">
                <el-form-item label="出生年月" prop="field129" label-width="100px">
                  <el-date-picker
                    v-model="formData.field156"
                    format="yyyy-MM-dd"
                    value-format="yyyy-MM-dd"
                    :style="{width: '100%'}"
                    placeholder="请选择日期"
                    clearable
                  />
                </el-form-item>
              </el-col>
            </el-row>
            <el-row :gutter="20">
              <el-col :span="12" style="width: 300px;">
                <el-form-item label="国籍" prop="field130" label-width="80px">
                  <el-select v-model="formData.country" placeholder="请选择国籍" clearable :style="{width: '100%'}">
                    <el-option
                      v-for="(item, index) in countryOptions"
                      :key="index"
                      :label="item.label"
                      :value="item.value"
                      :disabled="item.disabled"
                    />
                  </el-select>
                </el-form-item>
              </el-col>
              <el-col :span="12" style="width: 300px;">
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
              <el-col :span="12" style="width: 300px;">
                <el-form-item label="护照号码" prop="field130" label-width="80px">
                  <el-input v-model="formData.field130" placeholder="请输入护照号码" clearable :style="{width: '97%'}" />
                </el-form-item>
              </el-col>
            </el-row>
            <el-row :gutter="20" />
            <el-row :gutter="20">
              <el-col :span="6" style="width: 300px">
                <el-form-item label="车（船）次/航班号" prop="field131" label-width="100px">
                  <el-input
                    v-model="formData.field131"
                    placeholder="请输入车（船）次/航班号"
                    clearable
                    :style="{width: '100%'}"
                  />
                </el-form-item>
              </el-col>
              <el-col :span="8" style="width: 300px">
                <el-form-item label="车厢(牌)号" prop="carNum" label-width="100px">
                  <el-input
                    v-model="formData.carNum"
                    placeholder="请输入车厢(牌)号"
                    clearable
                    :style="{width: '100%'}"
                  />
                </el-form-item>
              </el-col>
              <el-col :span="8" style="width: 300px">
                <el-form-item label="座铺位号" prop="zpw" label-width="100px">
                  <el-input
                    v-model="formData.zpw"
                    placeholder="请输入做铺位号"
                    clearable
                    :style="{width: '100%'}"
                  />
                </el-form-item>
              </el-col>
            </el-row>
            <el-row :gutter="20" />

            <el-row :gutter="20">

              <el-col><template>在华居住地：</template></el-col>
            </el-row>
            <el-row :gutter="20">
              <el-col :span="6" style="width: 300px">
                <el-form-item label="省" prop="sf" lable-width="150px">
                  <el-select v-model="formData.sf" placeholder="请择选省" clearable :style="{width: '80%'}">
                    <el-option
                      v-for="(item, index) in sfOptions"
                      :key="index"
                      :label="item.label"
                      :value="item.value"
                      :disabled="item.disabled"
                    />
                  </el-select>
                </el-form-item>
              </el-col>
              <el-col :span="6" style="width: 300px">
                <el-form-item label="市县区" prop="city" lable-width="150px">
                  <el-select v-model="formData.city" placeholder="请选择市县区" clearable :style="{width: '70%'}">
                    <el-option
                      v-for="(item, index) in Options"
                      :key="index"
                      :label="item.label"
                      :value="item.value"
                      :disabled="item.disabled"
                    />
                  </el-select>
                </el-form-item>
              </el-col>
              <el-col :span="6" style="width: 300px">
                <el-form-item label="乡街道" prop="xjd">
                  <el-select v-model="formData.xjd" placeholder="请选择乡街道" clearable :style="{width: '70%'}">
                    <el-option
                      v-for="(item, index) in xjdOptions"
                      :key="index"
                      :label="item.label"
                      :value="item.value"
                      :disabled="item.disabled"
                    />
                  </el-select>
                </el-form-item>
              </el-col>
              <el-col :span="6" style="width: 300px;">
                <el-form-item label="村" prop="cun">
                  <el-input v-model="formData.cun" placeholder="请输入村" clearable :style="{width: '80%'}" />
                </el-form-item>
              </el-col>
            </el-row>

            <el-row>
              <el-col :span="24">
                <el-form-item label="酒店名称和地址" prop="hotel" lable-width="250px">
                  <el-input v-model="formData.hotel" placeholder="酒店名称和地址" clearable :style="{width: '60%'}" />
                </el-form-item>
              </el-col>
            </el-row>

            <el-row :gutter="20">
              <el-col :span="12" style="width: 500px">
                <el-form-item label="在华其他联系人" prop="lxr" lable-width="400px">
                  <el-input v-model="formData.lxr" placeholder="请输入在华其他联系人" clearable :style="{width: '100%'}" />
                </el-form-item>
              </el-col>
              <el-col :span="12">
                <el-form-item label="联系人电话" prop="lxrdh">
                  <el-input v-model="formData.lxrdh" placeholder="请输入联系人电话" clearable :style="{width: '60%'}" />
                </el-form-item>
              </el-col>
            </el-row>
            <el-col :span="23">
              <el-form-item label="初步排查结果" prop="field300">
                <el-checkbox-group v-model="formData.field300" size="medium">
                  <el-checkbox
                    v-for="(item, index) in field300Options"
                    :key="index"
                    :label="item.value"
                    :disabled="item.disabled"
                  >{{ item.label }}</el-checkbox>
                </el-checkbox-group>
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
              <el-form-item label="转运负责人" prop="field105">
                <el-input v-model="formData.field105" placeholder="请输入" clearable :style="{width: '100%'}" />
              </el-form-item>
            </el-col>
            <el-col :span="12">
              <el-form-item label="负责人电话" prop="field1055" lable-width="200px">
                <el-input v-model="formData.field1055" placeholder="请输入转运负责人电话" clearable :style="{width: '100%'}" />
              </el-form-item>
            </el-col>
            <!--          <el-col :span="12">-->
            <!--            <el-form-item label="拟送医院" prop="field107">-->
            <!--              <el-input v-model="formData.field107" placeholder="请输入拟送医院" clearable :style="{width: '100%'}" />-->
            <!--            </el-form-item>-->
            <!--          </el-col>-->
            <!--          <el-col :span="12">-->
            <!--            <el-form-item label="救护车医师" prop="field108">-->
            <!--              <el-input v-model="formData.field108" placeholder="救护车医师签字" clearable :style="{width: '100%'}" />-->
            <!--            </el-form-item>-->
            <!--          </el-col>-->
            <!--          <el-col :span="12">-->
            <!--            <el-form-item label="救护车医师电话" prop="field109">-->
            <!--              <el-input-->
            <!--                v-model="formData.field109"-->
            <!--                placeholder="请输入电话救护车医师电话"-->
            <!--                clearable-->
            <!--                :style="{width: '100%'}"-->
            <!--              />-->
            <!--            </el-form-item>-->
            <!--          </el-col>-->
            <el-col :span="12">
              <el-form-item label="接受医院" prop="field110">
                <el-input v-model="formData.field110" placeholder="请输入接受医院" clearable :style="{width: '100%'}" />
              </el-form-item>
            </el-col>
            <el-col :span="12">
              <el-form-item label="接受负责人" prop="field111">
                <el-input v-model="formData.field111" placeholder="接受负责人" clearable :style="{width: '100%'}" />
              </el-form-item>
            </el-col>
            <el-col :span="12">
              <el-form-item label="电话" prop="field114">
                <el-input v-model="formData.field114" placeholder="接受负责人电话" clearable :style="{width: '100%'}" />
              </el-form-item>
            </el-col>
            <el-col>
              <template>
                <p style="color: #606266">本移交记录单一式两联，一联由海关保存，另一联请转运负责人交给接受医院/机构接受负责人
                </p>
              </template>
            </el-col>
            <el-col :span="24">
              <el-form-item size="large">
                <el-button type="primary" size="mini" @click="submitForm">提交</el-button>
                <el-button size="mini" @click="resetForm">重置</el-button>
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

      field300Options: [{
        'label': '确诊病例',
        'value': 1
      }, {
        'label': '疑似病例',
        'value': 2
      }, {
        'label': '有发热等症状患者',
        'value': 3
      }, {
        'label': '密切接触者',
        'value': 4
      }, {
        'label': '无症状但有流行病学意义的患者',
        'value': 5
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
        lxrdh: undefined,
        lxr: undefined,
        city: undefined,
        sf: undefined,
        xjd: undefined,
        cun: undefined,
        field300: [],
        hotel: undefined,
        zpw: undefined,
        phone: undefined,
        carNum: undefined,
        otherDes: undefined,
        field101: undefined,
        field102: null,
        field103: undefined,
        field104: undefined,
        field105: undefined,
        field1055: undefined,
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
        field117: undefined,
        field127: undefined,
        field128: undefined,
        field129: undefined,
        field130: undefined,
        field131: undefined
      },
      rules: {
        lxr: [{
          required: true,
          message: '请输入联系人',
          trigger: 'blur'
        }],
        lxrdh: [{
          required: true,
          message: '请输入联系人电话',
          trigger: 'blur'
        }],
        hotel: [{
          required: true,
          message: '请填写酒店名称和地址',
          trigger: 'blur'
        }],
        sf: [{
          required: true,
          message: '请择选省',
          trigger: 'change'
        }],
        city: [{
          required: true,
          message: '请选择市县区',
          trigger: 'change'
        }],
        xjd: [{
          required: true,
          message: '请选择乡街道',
          trigger: 'change'
        }],
        cun: [{
          required: true,
          message: '请输入村',
          trigger: 'blur'
        }],
        field300: [{
          required: true,
          type: 'array',
          message: '请至少选择一个初步排查结果',
          trigger: 'change'
        }],
        zpw: [{
          required: true,
          message: '请输入座铺位号',
          trigger: 'blur'
        }],
        phone: [{
          required: true,
          message: '请输入电话号',
          trigger: 'blur'
        }],
        carNum: [{
          required: true,
          message: '请输入车牌号',
          trigger: 'blur'
        }],
        field131: [{
          required: true,
          message: '请输入车（船）次/航班号',
          trigger: 'blur'
        }],
        field127: [{
          required: true,
          message: '请输入姓名',
          trigger: 'blur'
        }],
        field128: [{
          required: true,
          message: '请选择性别',
          trigger: 'change'
        }],
        field129: [{
          required: true,
          message: '请选择证件类型',
          trigger: 'change'
        }],
        country: [{
          required: true,
          message: '请选择国籍',
          trigger: 'blur'
        }],
        field130: [{
          required: true,
          message: '请输入护照号码',
          trigger: 'blur'
        }],
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
        field1055: [{
          required: true,
          message: '请输入转运负责人电话',
          trigger: 'blur'
        }],
        field105: [{
          required: true,
          message: '请输入转运负责人',
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
          message: '接受负责人',
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
