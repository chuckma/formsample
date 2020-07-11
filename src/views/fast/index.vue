<template>
  <div>
    <el-form ref="elForm" :model="formData" :rules="rules" size="mini" label-width="100px" style="">
      <el-card class="box-card">
        <div slot="header" class="clearfix">
          <span>基本信息</span>
<!--          <el-button style="float: right; padding: 3px 0" type="text">操作按钮</el-button>-->
        </div>
        <el-row >
          <!--        <el-col :span="4"><div class="grid-content bg-purple">12313</div></el-col>-->
          <el-col :span="8" style="width: 400px">
            <el-form-item label="姓名" prop="field127" label-width="150px">
              <el-input
                v-model="formData.field127"
                placeholder="请输入姓名"
                show-word-limit
                clearable
                :style="{width: '100%'}"
              />
            </el-form-item>
          </el-col>
          <el-col :span="8" style="width: 400px;">
            <el-form-item label="性别" prop="field128" label-width="150px">
              <el-select v-model="formData.field128" placeholder="请选择性别" clearable :style="{width: '100%'}">
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
          <!--        <el-col :span="4"><div class="grid-content bg-purple"></div></el-col>-->
        </el-row>
        <el-row>
          <el-col :span="16" style="width: 400px;">
            <el-form-item label="证件类型" prop="field129" label-width="150px">
              <el-select v-model="formData.field129" placeholder="请选择证件类型" clearable :style="{width: '100%'}">
                <el-option
                  v-for="(item, index) in field129Options"
                  :key="index"
                  :label="item.label"
                  :value="item.value"
                  :disabled="item.disabled"
                />
              </el-select>
            </el-form-item>
          </el-col>
          <el-col :span="12" style="width: 400px;">
            <el-form-item label="证件号码" prop="field130" label-width="150px">
              <el-input v-model="formData.field130" placeholder="请输入证件号码" clearable :style="{width: '100%'}" />
            </el-form-item>
          </el-col>
        </el-row>
        <el-row>
          <el-col :span="12" style="width: 400px">
            <el-form-item label="车（船）次/航班号" prop="field131" label-width="150px">
              <el-input
                v-model="formData.field131"
                placeholder="请输入车（船）次/航班号"
                clearable
                :style="{width: '100%'}"
              />
            </el-form-item>
          </el-col>
          <el-col :span="12" style="width: 400px">
            <el-form-item label="检测体温" prop="field132" label-width="150px">
              <el-input v-model="formData.field132" placeholder="请输入检测体温" clearable :style="{width: '100%'}">
                <template slot="append">℃</template>
              </el-input>
            </el-form-item>
          </el-col>
        </el-row>
      </el-card>

<!--      <el-row>-->
<!--        <el-col style="color: #2b2f3a;font-weight: bold;margin: 20px 20px">流行病学调查</el-col>-->
<!--      </el-row>-->
      <el-card class="box-card">
        <div slot="header" class="clearfix">
          <span>流行病学调查</span>
<!--          <el-button style="float: right; padding: 3px 0" type="text">操作按钮</el-button>-->
        </div>
        <el-row>
          <el-col :span="24">
            <el-form-item label="14天内是否去过医院、剧院、餐厅、娱乐场所等公共场所？" prop="publicPlace" label-width="500px">
              <el-checkbox-group v-model="formData.publicPlace" size="medium">
                <el-checkbox
                  v-for="(item, index) in publicPlaceOptions"
                  :key="index"
                  :label="item.value"
                  :disabled="item.disabled"
                >{{ item.label }}</el-checkbox>
              </el-checkbox-group>
            </el-form-item>
          </el-col>
          <el-col :span="24">
            <el-form-item label="如果是，是否未佩戴口罩与其他人近距离（1米内）接触？" prop="field136" label-width="500px">
              <el-checkbox-group v-model="formData.field136" size="medium">
                <el-checkbox
                  v-for="(item, index) in field136Options"
                  :key="index"
                  :label="item.value"
                  :disabled="item.disabled"
                >{{ item.label }}</el-checkbox>
              </el-checkbox-group>
            </el-form-item>
          </el-col>
          <el-col :span="24">
            <el-form-item label="14天内是否参加过其他聚集性活动？" prop="field137" label-width="500px">
              <el-checkbox-group v-model="formData.field137" size="medium">
                <el-checkbox
                  v-for="(item, index) in field137Options"
                  :key="index"
                  :label="item.value"
                  :disabled="item.disabled"
                >{{ item.label }}</el-checkbox>
              </el-checkbox-group>
            </el-form-item>
          </el-col>
          <el-col :span="24">
            <el-form-item label="来华（归国）的目的是否与就医有关？" prop="field138" label-width="500px">
              <el-checkbox-group v-model="formData.field138" size="medium">
                <el-checkbox
                  v-for="(item, index) in field138Options"
                  :key="index"
                  :label="item.value"
                  :disabled="item.disabled"
                >{{ item.label }}</el-checkbox>
              </el-checkbox-group>
            </el-form-item>
          </el-col>
          <el-col :span="24">
            <el-form-item label="14天内是否接触、处理或食用过野生动物？（水生动物除外）" prop="field139" label-width="500px">
              <el-checkbox-group v-model="formData.field139" size="medium">
                <el-checkbox
                  v-for="(item, index) in field139Options"
                  :key="index"
                  :label="item.value"
                  :disabled="item.disabled"
                >{{ item.label }}</el-checkbox>
              </el-checkbox-group>
            </el-form-item>
          </el-col>
          <el-col :span="16">
            <el-form-item label="其他相关因素调查" prop="field140" label-width="400px">
              <el-input
                v-model="formData.field140"
                type="textarea"
                placeholder="请输入其他相关因素调查"
                :autosize="{minRows: 4, maxRows: 4}"
                :style="{width: '100%'}"
              />
            </el-form-item>
          </el-col>
        </el-row>
      </el-card>

      <el-card class="box-card">
        <div slot="header" class="clearfix">
          <span>初步判断意见</span>
        </div>
<!--        <el-row>-->
<!--          <el-col :span="6">-->
<!--            <el-form-item label="无明显接触史或暴露史" prop="field143" label-width="200px">-->

<!--              <el-checkbox-group v-model="formData.field143" size="medium">-->
<!--                <el-checkbox-->
<!--                  v-for="(item, index) in field143Options"-->
<!--                  :key="index"-->
<!--                  :label="item.value"-->
<!--                  :disabled="item.disabled"-->
<!--                >{{ item.label }}</el-checkbox>-->
<!--              </el-checkbox-group>-->
<!--            </el-form-item>-->
<!--          </el-col>-->
<!--          <el-col :span="6">-->
<!--          <el-form-item label="密切接触者" prop="field148"  label-width="200px">-->

<!--              <el-checkbox-group v-model="formData.field143" size="medium">-->
<!--                <el-checkbox-->
<!--                  v-for="(item, index) in field143Options"-->
<!--                  :key="index"-->
<!--                  :label="item.value"-->
<!--                  :disabled="item.disabled"-->
<!--                >{{ item.label }}</el-checkbox>-->
<!--              </el-checkbox-group>-->
<!--            </el-form-item>-->
<!--          </el-col>-->
<!--          <el-col :span="6">-->
<!--            <el-form-item label="一般接触者" prop="field149"  label-width="200px">-->
<!--              <el-checkbox-group v-model="formData.field143" size="medium">-->
<!--                <el-checkbox-->
<!--                  v-for="(item, index) in field143Options"-->
<!--                  :key="index"-->
<!--                  :label="item.value"-->
<!--                  :disabled="item.disabled"-->
<!--                >{{ item.label }}</el-checkbox>-->
<!--              </el-checkbox-group>-->
<!--            </el-form-item>-->
<!--          </el-col>-->
<!--          <el-col :span="6">-->
<!--            <el-form-item label="其他情况" prop="field150"  label-width="200px">-->
<!--            <el-checkbox-group v-model="formData.field143" size="medium">-->
<!--                <el-checkbox-->
<!--                  v-for="(item, index) in field143Options"-->
<!--                  :key="index"-->
<!--                  :label="item.value"-->
<!--                  :disabled="item.disabled"-->
<!--                >{{ item.label }}</el-checkbox>-->
<!--              </el-checkbox-group>-->
<!--            </el-form-item>-->
<!--          </el-col>-->
<!--        </el-row>-->
<!--        <el-form-item label="判断意见" prop="field143">-->
<!--          <el-checkbox-group v-model="formData.field143">-->
<!--            <el-checkbox label="无明显接触史或暴露史" name="field143"></el-checkbox>-->
<!--            <el-checkbox label="密切接触者" name="field143"></el-checkbox>-->
<!--            <el-checkbox label="一般接触者" name="field143"></el-checkbox>-->
<!--            <el-checkbox label="其他情况" name="field143"></el-checkbox>-->
<!--          </el-checkbox-group>-->
<!--        </el-form-item>-->

        <el-form-item label="判断意见" prop="field143">
        <el-radio-group v-model="formData.field143" @change="handlerRadio">
          <el-radio label="无明显接触史或暴露史"></el-radio>
          <el-radio label="密切接触者"></el-radio>
          <el-radio label="一般接触者"></el-radio>
          <el-radio label="其他情况"></el-radio>
        </el-radio-group>
        </el-form-item>
        <el-form-item label="活动形式" prop="desc" v-if="otherDesShow">
          <el-input type="textarea" v-model="formData.otherDes" placeholder="请输入其他情况的说明"></el-input>
        </el-form-item>
      </el-card>

      <el-card class="box-card">
        <div slot="header" class="clearfix">
          <span></span>
        </div>
        <el-row>
          <el-col :span="8" >
            <el-form-item label="流调人员签名" prop="field153"  label-width="150px">
              <el-input v-model="formData.field153" placeholder="请输入流调人员签名" clearable :style="{width: '100%'}" />
            </el-form-item>
          </el-col>
          <el-col :span="8" >
            <el-form-item label="带班人员签名" prop="field154" label-width="150px" >
              <el-input v-model="formData.field154" placeholder="请输入带班人员签名" clearable :style="{width: '100%'}" />
            </el-form-item>
          </el-col>
          <el-col :span="8" >
            <el-form-item label="调查日期" prop="field156" label-width="150px" >
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

      </el-card>

      <el-form-item size="large" style="float: right">
        <el-button type="primary" @click="submitForm" size="mini">提交</el-button>
        <el-button @click="resetForm" size="mini">重置</el-button>
      </el-form-item>
    </el-form>
  </div>
</template>
<script>
export default {
  components: {},
  props: [],
  data() {
    return {
      formData: {
        otherDes: undefined,
        field127: undefined,
        field128: undefined,
        field129: undefined,
        field130: undefined,
        field131: undefined,
        field132: undefined,
        publicPlace: [],
        field136: [],
        field137: [],
        field138: [],
        field139: [],
        field140: undefined,
        field143: [],
        field148: [],
        field149: [],
        field150: [],
        field153: undefined,
        field154: undefined,
        field156: undefined
      },
      rules: {
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
        field130: [{
          required: true,
          message: '请输入证件号码',
          trigger: 'blur'
        }],
        field131: [{
          required: true,
          message: '请输入车（船）次/航班号',
          trigger: 'blur'
        }],
        field132: [{
          required: true,
          message: '请输入检测体温',
          trigger: 'blur'
        }],
        publicPlace: [{
          required: true,
          type: 'array',
          message: '请至少选择一个',
          trigger: 'change'
        }],
        field136: [{
          required: true,
          type: 'array',
          message: '请至少选择一个',
          trigger: 'change'
        }],
        field137: [{
          required: true,
          type: 'array',
          message: '请至少选择一个',
          trigger: 'change'
        }],
        field138: [{
          required: true,
          type: 'array',
          message: '请至少选择一个',
          trigger: 'change'
        }],
        field139: [{
          required: true,
          type: 'array',
          message: '请至少选择一个',
          trigger: 'change'
        }],
        field140: [{
          required: true,
          message: '请输入其他相关因素调查',
          trigger: 'blur'
        }],
        field143: [{
          // type: 'array',
          required: true,
          message: '请选择一个诊断意见',
          trigger: 'change'
        }],
        // field143: [{
        //   required: true,
        //   type: 'array',
        //   message: '请至少选择一个',
        //   trigger: 'change'
        // }],
        field148: [{
          required: true,
          type: 'array',
          message: '请至少选择一个',
          trigger: 'change'
        }],
        field149: [{
          required: true,
          type: 'array',
          message: '请至少选择一个',
          trigger: 'change'
        }],
        field150: [{
          required: true,
          type: 'array',
          message: '请至少选择一个其他情况',
          trigger: 'change'
        }],
        field153: [{
          required: true,
          message: '请输入流调人员签名',
          trigger: 'blur'
        }],
        field154: [{
          required: true,
          message: '请输入带班人员签名',
          trigger: 'blur'
        }],
        field156: [{
          required: true,
          message: '请选择日期选择',
          trigger: 'change'
        }]
      },
      otherDesShow: false,
      field128Options: [{
        'label': '男',
        'value': 1
      }, {
        'label': '女',
        'value': 2
      }],
      field129Options: [{
        'label': '居民身份证',
        'value': 1
      }, {
        'label': '护照',
        'value': 2
      }, {
        'label': '旅行证',
        'value': ''
      }, {
        'label': '出入境通行证',
        'value': ''
      }],
      publicPlaceOptions: [{
        'label': '是',
        'value': 1
      }, {
        'label': '否',
        'value': 2
      }],
      field136Options: [{
        'label': '是',
        'value': 1
      }, {
        'label': '否',
        'value': 2
      }],
      field137Options: [{
        'label': '是',
        'value': 1
      }, {
        'label': '否',
        'value': 2
      }],
      field138Options: [{
        'label': '是',
        'value': 1
      }, {
        'label': '否',
        'value': 2
      }],
      field139Options: [{
        'label': '是',
        'value': 1
      }, {
        'label': '否',
        'value': 2
      }],
      field143Options: [{
        'label': '',
        'value': ''
      }],
      field148Options: [{
        'label': '',
        'value': ''
      }],
      field149Options: [{
        'label': '',
        'value': ''
      }],
      field150Options: [{
        'label': '',
        'value': ''
      }]
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
    },
    handlerRadio(value) {
      if (value === '其他情况') {
        otherDesShow = true
      }
    }
  }
}

</script>
<style>
</style>
