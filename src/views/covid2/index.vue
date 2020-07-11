<template>
  <el-row>
    <el-col :span="12">
      <div class="grid-content bg-purple">
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
        />
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
      <div class="grid-content bg-purple-light">
        <el-form ref="elForm" :model="formData" :rules="rules" size="mini">
          <el-card class="box-card">
            <div slot="header" class="clearfix">
              <span>基本信息</span>
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
            </el-row>
            <el-row :gutter="20">
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
              <el-col :span="12" style="width: 300px;">
                <el-form-item label="护照号码" prop="field130" label-width="80px">
                  <el-input v-model="formData.field130" placeholder="请输入护照号码" clearable :style="{width: '97%'}" />
                </el-form-item>
              </el-col>
            </el-row>
            <el-row :gutter="20" />
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
                <el-form-item label="职业" prop="zy" label-width="80px">
                  <el-input v-model="formData.zy" placeholder="请填写职业" clearable :style="{width: '100%'}" />
                </el-form-item>
              </el-col>
              <el-col :span="16" style="width: 300px;">
                <el-form-item label="出入境时间" prop="field157" label-width="100px">
                  <el-date-picker
                    v-model="formData.field157"
                    format="yyyy-MM-dd HH:mm"
                    value-format="yyyy-MM-dd HH:mm"
                    :style="{width: '100%'}"
                    placeholder="请选择时间"
                    clearable
                    type="datetime"
                  />
                </el-form-item>
              </el-col>
              <el-col :span="12" style="width: 300px">
                <el-form-item label="车（船）次/航班号" prop="field131" label-width="100px">
                  <el-input
                    v-model="formData.field131"
                    placeholder="请输入车（船）次/航班号"
                    clearable
                    :style="{width: '100%'}"
                  />
                </el-form-item>
              </el-col>
            </el-row>
            <el-row :gutter="20">

              <el-col :span="12" style="width: 300px">
                <el-form-item label="车厢(牌)号" prop="carNum" label-width="100px">
                  <el-input
                    v-model="formData.carNum"
                    placeholder="请输入车厢(牌)号"
                    clearable
                    :style="{width: '100%'}"
                  />
                </el-form-item>
              </el-col>
              <el-col :span="12" style="width: 300px">
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
            <el-row :gutter="20">
              <el-col :span="12" style="width: 300px">
                <el-form-item label="在华其他联系人" prop="lxr">
                  <el-input v-model="formData.lxr" placeholder="请输入在华其他联系人" clearable :style="{width: '50%'}" />
                </el-form-item>
              </el-col>
              <el-col :span="12">
                <el-form-item label="联系人电话" prop="lxrdh">
                  <el-input v-model="formData.lxrdh" placeholder="请输入联系人电话" clearable :style="{width: '60%'}" />
                </el-form-item>
              </el-col>
            </el-row>
            <el-row>
              <!--              <el-col :span="24">-->
              <!--                <el-form-item label="个案发现渠道" prop="gafxqd">-->
              <!--                  <el-radio-group v-model="formData.gafxqd" size="medium">-->
              <!--                    <el-radio-->
              <!--                      v-for="(item, index) in gafxqdOptions"-->
              <!--                      :key="index"-->
              <!--                      :label="item.value"-->
              <!--                      :disabled="item.disabled"-->
              <!--                    >{{ item.label }}</el-radio>-->
              <!--                  </el-radio-group>-->
              <!--                </el-form-item>-->
              <!--              </el-col>-->

              <el-row>
                <el-col><template slot="">1. 既往病史
                </template></el-col>
              </el-row>
              <el-row>
                <el-col :span="24">
                  <el-form-item label="" prop="jwbs">
                    <el-checkbox-group v-model="formData.jwbs" size="medium">
                      <el-checkbox
                        v-for="(item, index) in jwbsOptions"
                        :key="index"
                        :label="item.value"
                        :disabled="item.disabled"
                      >{{ item.label }}</el-checkbox>
                    </el-checkbox-group>
                  </el-form-item>
                </el-col>
              </el-row>

              <el-col :span="12" style="width: 350px">
                <el-form-item label="首次症状日期" prop="sczzrq" label-width="110px">
                  <el-date-picker
                    v-model="formData.sczzrq"
                    format="yyyy-MM-dd"
                    value-format="yyyy-MM-dd"
                    :style="{width: '100%'}"
                    placeholder="请选择首次症状日期"
                    clearable
                  />
                </el-form-item>
              </el-col>
            </el-row>

          </el-card>

          <el-card class="box-card">
            <div slot="header" class="clearfix">
              <span>临床表现</span>
            </div>
            <el-row :gutter="20">
              <el-col :span="24" style="width: 500px;">
                <el-form-item label="腋温测量最高  " prop="twds" lable-width="250px">
                  <el-input v-model="formData.twds" placeholder="请输入腋温测量最高  " clearable :style="{width: '250px'}">
                    <template slot="append">℃</template>
                  </el-input>
                </el-form-item>
              </el-col>

              <el-col :span="24">
                <el-form-item label="症状" prop="zzbx">
                  <el-checkbox-group v-model="formData.zzbx" size="medium">
                    <el-checkbox
                      v-for="(item, index) in zzbxOptions"
                      :key="index"
                      :label="item.value"
                      :disabled="item.disabled"
                    >{{ item.label }}</el-checkbox>
                  </el-checkbox-group>
                </el-form-item>
              </el-col>
            </el-row>
          </el-card>
          <el-card class="box-card">
            <div slot="header" class="clearfix">
              <span>流行病学因素调查</span>
            </div>

            <el-row>
              <el-col :span="24">
                <el-form-item label="出现症状前14天内 □是 □否 去过湖北省的旅行史或居住史" prop="field200">
                  <el-checkbox-group v-model="formData.field200" size="medium">
                    <el-checkbox
                      v-for="(item, index) in field200Options"
                      :key="index"
                      :label="item.value"
                      :disabled="item.disabled"
                    >{{ item.label }}</el-checkbox>
                  </el-checkbox-group>
                </el-form-item>
              </el-col>
            </el-row>

            <el-row>
              <el-col :span="24">
                <el-form-item label="出现症状前14天内是否 接触过来自湖北省的发热或有呼吸道症状的患者" prop="field201">
                  <el-checkbox-group v-model="formData.field201" size="medium">
                    <el-checkbox
                      v-for="(item, index) in field201Options"
                      :key="index"
                      :label="item.value"
                      :disabled="item.disabled"
                    >{{ item.label }}</el-checkbox>
                  </el-checkbox-group>
                </el-form-item>
              </el-col>
            </el-row>

            <el-row>
              <el-col :span="24">
                <el-form-item label="出现症状前14天内是否接触过来自湖北省的发热或有呼吸道症状的患者" prop="field245">
                  <el-checkbox-group v-model="formData.field245" size="medium">
                    <el-checkbox
                      v-for="(item, index) in field245Options"
                      :key="index"
                      :label="item.value"
                      :disabled="item.disabled"
                    >{{ item.label }}</el-checkbox>
                  </el-checkbox-group>
                </el-form-item>
              </el-col>
            </el-row>

            <el-row>
              <el-col :span="24">
                <el-form-item label="出现症状前14天内是否 接触过有病例报告社区的发热或有呼吸道症状的患者" prop="field246">
                  <el-checkbox-group v-model="formData.field246" size="medium">
                    <el-checkbox
                      v-for="(item, index) in field201Options"
                      :key="index"
                      :label="item.value"
                      :disabled="item.disabled"
                    >{{ item.label }}</el-checkbox>
                  </el-checkbox-group>
                </el-form-item>
              </el-col>
            </el-row>

            <el-row>
              <el-col :span="24">
                <el-form-item label=" 有无 聚集性发病或接触过新型冠状病毒感染者" prop="field247">
                  <el-checkbox-group v-model="formData.field247" size="medium">
                    <el-checkbox
                      v-for="(item, index) in field215Options"
                      :key="index"
                      :label="item.value"
                      :disabled="item.disabled"
                    >{{ item.label }}</el-checkbox>
                  </el-checkbox-group>
                </el-form-item>
              </el-col>
            </el-row>

            <el-row>
              <el-col :span="21">
                <el-form-item label="与上面病人密切接触人员" prop="field210">
                  <el-input
                    v-model="formData.field210"
                    type="textarea"
                    placeholder="请输入与上面病人密切接触人员"
                    :autosize="{minRows: 4, maxRows: 4}"
                    :style="{width: '100%'}"
                  />
                </el-form-item>
              </el-col>
            </el-row>
            <el-col :span="21">
              <el-form-item label="共同暴露人员" prop="field211">
                <el-input
                  v-model="formData.field211"
                  type="textarea"
                  placeholder="请输入共同暴露人员"
                  :autosize="{minRows: 4, maxRows: 4}"
                  :style="{width: '100%'}"
                />
              </el-form-item>
            </el-col>
            <el-row />

            <!--<el-row>
              <el-col :span="21">
                <el-form-item label="病前14天内 是 否 去过酒吧、剧院、餐厅、医院、体育场馆、娱乐场所等公共场所" prop="field212">
                  <el-checkbox-group v-model="formData.field212" size="medium">
                    <el-checkbox
                      v-for="(item, index) in field212Options"
                      :key="index"
                      :label="item.value"
                      :disabled="item.disabled"
                    >{{ item.label }}</el-checkbox>
                  </el-checkbox-group>
                </el-form-item>
              </el-col>
            </el-row>

            <el-row>
              <el-col :span="21">
                <el-form-item label="发病前14天内 是 否 乘坐其他飞机、客（邮）轮、列车、地铁、客运汽车等公共交通工具" prop="field213">
                  <el-checkbox-group v-model="formData.field213" size="medium">
                    <el-checkbox
                      v-for="(item, index) in field213Options"
                      :key="index"
                      :label="item.value"
                      :disabled="item.disabled"
                    >{{ item.label }}</el-checkbox>
                  </el-checkbox-group>
                </el-form-item>
              </el-col>
            </el-row>

            <el-row>
              <el-col :span="21">
                <el-form-item label="发病前14天内 是 否 在公共室内环境下有效佩戴口罩，良好的手卫生习惯" prop="field214">
                  <el-checkbox-group v-model="formData.field214" size="medium">
                    <el-checkbox
                      v-for="(item, index) in field214Options"
                      :key="index"
                      :label="item.value"
                      :disabled="item.disabled"
                    >{{ item.label }}</el-checkbox>
                  </el-checkbox-group>
                </el-form-item>
              </el-col>
            </el-row>

            <el-row>
              <el-col :span="21">
                <el-form-item label="家庭、单位、旅行团等有 无2例及以上发热或呼吸道症状的病例" prop="field215">
                  <el-checkbox-group v-model="formData.field215" size="medium">
                    <el-checkbox
                      v-for="(item, index) in field215Options"
                      :key="index"
                      :label="item.value"
                      :disabled="item.disabled"
                    >{{ item.label }}</el-checkbox>
                  </el-checkbox-group>
                </el-form-item>
              </el-col>
            </el-row>

            <el-row>

              <el-col :span="21">
                <el-form-item label="来华（归国）的目的是 否与就医有关；" prop="field216">
                  <el-checkbox-group v-model="formData.field216" size="medium">
                    <el-checkbox
                      v-for="(item, index) in field216Options"
                      :key="index"
                      :label="item.value"
                      :disabled="item.disabled"
                    >{{ item.label }}</el-checkbox>
                  </el-checkbox-group>
                </el-form-item>
              </el-col>
            </el-row>

            <el-row>
              <el-col :span="21">
                <el-form-item label="发病前近14日内，是 否曾接受过新型冠状病毒检测" prop="field217">
                  <el-checkbox-group v-model="formData.field217" size="medium">
                    <el-checkbox
                      v-for="(item, index) in field217Options"
                      :key="index"
                      :label="item.value"
                      :disabled="item.disabled"
                    >{{ item.label }}</el-checkbox>
                  </el-checkbox-group>
                </el-form-item>
              </el-col>
            </el-row>

            <el-row>
              <el-col :span="21">
                <el-form-item label="如接受过，则检测结果为" prop="field218">
                  <el-radio-group v-model="formData.field218" size="medium">
                    <el-radio
                      v-for="(item, index) in field218Options"
                      :key="index"
                      :label="item.value"
                      :disabled="item.disabled"
                    >{{ item.label }}</el-radio>
                  </el-radio-group>
                </el-form-item>
              </el-col>
            </el-row>-->

            <el-row>
              <el-col :span="21">
                <el-form-item label="接触、处理或食用过活的或死的野生动物和生的及未煮熟的动物肉" prop="field219">
                  <el-checkbox-group v-model="formData.field219" size="medium">
                    <el-checkbox
                      v-for="(item, index) in field219Options"
                      :key="index"
                      :label="item.value"
                      :disabled="item.disabled"
                    >{{ item.label }}</el-checkbox>
                  </el-checkbox-group>
                </el-form-item>
              </el-col>
            </el-row>

            <el-row>
              <el-col :span="21">
                <el-form-item label="如果有，具体接触情况是" prop="field220">
                  <el-input
                    v-model="formData.field220"
                    type="textarea"
                    placeholder="请输入具体接触情况"
                    :autosize="{minRows: 4, maxRows: 4}"
                    :style="{width: '100%'}"
                  />
                </el-form-item>
              </el-col>
            </el-row>

            <!--<el-row>
              <el-col :span="21">
                <el-form-item label="发病前14天内 有 无 感染环境暴露史？" prop="field221">
                  <el-checkbox-group v-model="formData.field221" size="medium">
                    <el-checkbox
                      v-for="(item, index) in field221Options"
                      :key="index"
                      :label="item.value"
                      :disabled="item.disabled"
                    >{{ item.label }}</el-checkbox>
                  </el-checkbox-group>
                </el-form-item>
              </el-col>
            </el-row>

            <el-row>
              <el-col :span="21">
                <el-form-item label="如果有，具体接触情况是" prop="field222">
                  <el-input
                    v-model="formData.field222"
                    type="textarea"
                    placeholder="请输入具体接触情况"
                    :autosize="{minRows: 4, maxRows: 4}"
                    :style="{width: '100%'}"
                  />
                </el-form-item>
              </el-col>
            </el-row>

            <el-row>
              <el-col :span="21">
                <el-form-item label="有 无蚊虫叮咬史" prop="field223">
                  <el-checkbox-group v-model="formData.field223" size="medium">
                    <el-checkbox
                      v-for="(item, index) in field223Options"
                      :key="index"
                      :label="item.value"
                      :disabled="item.disabled"
                    >{{ item.label }}</el-checkbox>
                  </el-checkbox-group>
                </el-form-item>
              </el-col>
            </el-row>-->

            <el-row>
              <el-col :span="21">
                <el-form-item label="是 否从事动物饲养、宰杀、捕捉或标本制作工作" prop="field224">
                  <el-checkbox-group v-model="formData.field224" size="medium">
                    <el-checkbox
                      v-for="(item, index) in field224Options"
                      :key="index"
                      :label="item.value"
                      :disabled="item.disabled"
                    >{{ item.label }}</el-checkbox>
                  </el-checkbox-group>
                </el-form-item>
              </el-col>
            </el-row>

            <el-row>
              <el-col :span="21">
                <el-form-item label="如果是，具体接触情况是" prop="field225">
                  <el-input
                    v-model="formData.field225"
                    type="textarea"
                    placeholder="请输入具体接触情况"
                    :autosize="{minRows: 4, maxRows: 4}"
                    :style="{width: '100%'}"
                  />
                </el-form-item>
              </el-col>
            </el-row>

            <el-row>
              <el-col :span="21">
                <el-form-item label="是 否从事病原生物学研究或医务工作" prop="field226">
                  <el-checkbox-group v-model="formData.field226" size="medium">
                    <el-checkbox
                      v-for="(item, index) in field226Options"
                      :key="index"
                      :label="item.value"
                      :disabled="item.disabled"
                    >{{ item.label }}</el-checkbox>
                  </el-checkbox-group>
                </el-form-item>
              </el-col>
            </el-row>

            <!--            <el-row>-->
            <!--              <el-col :span="21">-->
            <!--                <el-form-item label="如果是，具体接触情况是" prop="field227">-->
            <!--                  <el-input-->
            <!--                    v-model="formData.field227"-->
            <!--                    type="textarea"-->
            <!--                    placeholder="请输入具体接触情况"-->
            <!--                    :autosize="{minRows: 4, maxRows: 4}"-->
            <!--                    :style="{width: '100%'}"-->
            <!--                  />-->
            <!--                </el-form-item>-->
            <!--              </el-col>-->
            <!--            </el-row>-->

            <el-row>
              <el-col :span="21">
                <el-form-item label="有无传染病史" prop="field228">
                  <el-checkbox-group v-model="formData.field228" size="medium">
                    <el-checkbox
                      v-for="(item, index) in field228Options"
                      :key="index"
                      :label="item.value"
                      :disabled="item.disabled"
                    >{{ item.label }}</el-checkbox>
                  </el-checkbox-group>
                </el-form-item>
              </el-col>
            </el-row>

            <el-row>
              <el-col :span="21">
                <el-form-item label="如果有，具体情况是" prop="field229">
                  <el-input
                    v-model="formData.field229"
                    type="textarea"
                    placeholder="请输入具体情况"
                    :autosize="{minRows: 4, maxRows: 4}"
                    :style="{width: '100%'}"
                  />
                </el-form-item>
              </el-col>
            </el-row>

            <!--<el-row>
              <el-col :span="21">
                <el-form-item label="有 无 怀孕" prop="field230">
                  <el-checkbox-group v-model="formData.field230" size="medium">
                    <el-checkbox
                      v-for="(item, index) in field230Options"
                      :key="index"
                      :label="item.value"
                      :disabled="item.disabled"
                    >{{ item.label }}</el-checkbox>
                  </el-checkbox-group>
                </el-form-item>
              </el-col>
            </el-row>

            <el-row>
              <el-col :span="21">
                <el-form-item label="有 无 晕机（车、船）史" prop="field231">
                  <el-checkbox-group v-model="formData.field231" size="medium">
                    <el-checkbox
                      v-for="(item, index) in field231Options"
                      :key="index"
                      :label="item.value"
                      :disabled="item.disabled"
                    >{{ item.label }}</el-checkbox>
                  </el-checkbox-group>
                </el-form-item>
              </el-col>
            </el-row>-->

            <el-row>
              <el-col :span="21">
                <el-form-item label="近期有无用退烧药" prop="field232">
                  <el-checkbox-group v-model="formData.field232" size="medium">
                    <el-checkbox
                      v-for="(item, index) in field232Options"
                      :key="index"
                      :label="item.value"
                      :disabled="item.disabled"
                    >{{ item.label }}</el-checkbox>
                  </el-checkbox-group>
                </el-form-item>
              </el-col>
            </el-row>

            <el-row>
              <el-col :span="21">
                <el-form-item label="如果有，具体用药情况是" prop="field233">
                  <el-input
                    v-model="formData.field233"
                    type="textarea"
                    placeholder="请输入用药情况"
                    :autosize="{minRows: 4, maxRows: 4}"
                    :style="{width: '100%'}"
                  />
                </el-form-item>
              </el-col>
            </el-row>

            <!--            <el-row>-->
            <!--              <el-col :span="21">-->
            <!--                <el-form-item label="是 否曾住院诊断" prop="field234">-->
            <!--                  <el-checkbox-group v-model="formData.field234" size="medium">-->
            <!--                    <el-checkbox-->
            <!--                      v-for="(item, index) in field234Options"-->
            <!--                      :key="index"-->
            <!--                      :label="item.value"-->
            <!--                      :disabled="item.disabled"-->
            <!--                    >{{ item.label }}</el-checkbox>-->
            <!--                  </el-checkbox-group>-->
            <!--                </el-form-item>-->
            <!--              </el-col>-->
            <!--            </el-row>-->

            <!--            <el-row>-->
            <!--              <el-col :span="21">-->
            <!--                <el-form-item label="如果是，具体诊断结果是" prop="field235">-->
            <!--                  <el-input-->
            <!--                    v-model="formData.field235"-->
            <!--                    type="textarea"-->
            <!--                    placeholder="请输入诊断结果"-->
            <!--                    :autosize="{minRows: 4, maxRows: 4}"-->
            <!--                    :style="{width: '100%'}"-->
            <!--                  />-->
            <!--                </el-form-item>-->
            <!--              </el-col>-->
            <!--            </el-row>-->

            <!--            <el-row>-->
            <!--              <el-col :span="21">-->
            <!--                <el-form-item label="近期有 无输血献血" prop="field236">-->
            <!--                  <el-checkbox-group v-model="formData.field236" size="medium">-->
            <!--                    <el-checkbox-->
            <!--                      v-for="(item, index) in field236Options"-->
            <!--                      :key="index"-->
            <!--                      :label="item.value"-->
            <!--                      :disabled="item.disabled"-->
            <!--                    >{{ item.label }}</el-checkbox>-->
            <!--                  </el-checkbox-group>-->
            <!--                </el-form-item>-->
            <!--              </el-col>-->
            <!--            </el-row>-->

            <!--            <el-row>-->
            <!--              <el-col :span="21">-->
            <!--                <el-form-item label="如果有，具体献血情况是" prop="field237">-->
            <!--                  <el-input-->
            <!--                    v-model="formData.field237"-->
            <!--                    type="textarea"-->
            <!--                    placeholder="请输入献血情况"-->
            <!--                    :autosize="{minRows: 4, maxRows: 4}"-->
            <!--                    :style="{width: '100%'}"-->
            <!--                  />-->
            <!--                </el-form-item>-->
            <!--              </el-col>-->
            <!--            </el-row>-->

            <!--            <el-row>-->
            <!--              <el-col :span="21">-->
            <!--                <el-form-item label="有 无 过敏史" prop="field238">-->
            <!--                  <el-checkbox-group v-model="formData.field238" size="medium">-->
            <!--                    <el-checkbox-->
            <!--                      v-for="(item, index) in field238Options"-->
            <!--                      :key="index"-->
            <!--                      :label="item.value"-->
            <!--                      :disabled="item.disabled"-->
            <!--                    >{{ item.label }}</el-checkbox>-->
            <!--                  </el-checkbox-group>-->
            <!--                </el-form-item>-->
            <!--              </el-col>-->
            <!--            </el-row>-->

            <!--            <el-row>-->
            <!--              <el-col :span="21">-->
            <!--                <el-form-item label="如果有，具体过敏情形" prop="field239">-->
            <!--                  <el-input-->
            <!--                    v-model="formData.field239"-->
            <!--                    type="textarea"-->
            <!--                    placeholder="请输入过敏情形"-->
            <!--                    :autosize="{minRows: 4, maxRows: 4}"-->
            <!--                    :style="{width: '100%'}"-->
            <!--                  />-->
            <!--                </el-form-item>-->
            <!--              </el-col>-->
            <!--            </el-row>-->

            <el-row>
              <el-col :span="21">
                <el-form-item label="其他相关因素调查" prop="field240">
                  <el-input
                    v-model="formData.field240"
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
            <el-row>
              <el-col :span="21">
                <el-form-item label="初步判断及病例处理意见" prop="field241">
                  <el-radio-group v-model="formData.field241" size="medium" @change="handlerRadio">
                    <el-radio
                      v-for="(item, index) in field241Options"
                      :key="index"
                      :label="item.value"
                      :disabled="item.disabled"
                    >{{ item.label }}</el-radio>
                  </el-radio-group>
                </el-form-item>
              </el-col>
            </el-row>
            <el-row>
              <el-col>
                按照其他途径<el-input v-model="formData.field2412" placeholder="请输入" type="input" clearable :style="{width: '200px',height:'20px', lineHeight: '20px'}" />传播传染病进行排查和处置
              </el-col>
              <el-col :span="24" style="margin-top: 4px">
                <el-input v-model="formData.field2411" placeholder="请输入其他诊断结果" type="textarea" clearable :style="{width: '100%'}" />
              </el-col>

            </el-row>
          </el-card>

          <el-card class="box-card">
            <div slot="header" class="clearfix">
              <span />
            </div>
            <el-row :gutter="2">
              <el-col :span="8">
                <el-form-item label="流调人员签名" prop="field153" label-width="110px">
                  <el-input v-model="formData.field153" placeholder="请输入流调人员签名" clearable :style="{width: '100%'}" />
                </el-form-item>
              </el-col>
              <el-col :span="8">
                <el-form-item label="带班人员签名" prop="field154" label-width="110px">
                  <el-input v-model="formData.field154" placeholder="请输入带班人员签名" clearable :style="{width: '100%'}" />
                </el-form-item>
              </el-col>
              <el-col :span="8">
                <el-form-item label="调查日期" prop="field156" label-width="80px">
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
            <el-button type="primary" size="mini" @click="submitForm">提交</el-button>
            <el-button size="mini" @click="resetForm">重置</el-button>
          </el-form-item>
        </el-form>
      </div>
    </el-col>
  </el-row>

</template>

<style>
  .el-table .warning-row {
    background: oldlace;
  }

  .el-table .success-row {
    background: #f0f9eb;
  }
</style>

<script>
export default {
  data() {
    return {
      zdjg: false,
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
        name: '王小虎',
        sex: '男',
        country: '中国',
        zjhm: '10012231312131',
        port: 'xxx口岸xx通道',
        outOrIn: '入境',
        passTime: '2020-07-10 22:22'
      }, {
        num: '4',
        name: '王小虎',
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
      portOptions: [{
        'label': 'A通道',
        'value': 1
      }, {
        'label': 'B通道',
        'value': 2
      }],

      formData: {
        zpw: undefined,
        phone: undefined,
        carNum: undefined,
        otherDes: undefined,
        field127: '',
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
        field156: undefined,
        country: undefined,
        zy: undefined,

        sf: undefined,
        city: undefined,
        xjd: undefined,
        cun: undefined,
        lxr: undefined,
        lxrdh: undefined,
        gafxqd: 1,
        twds: undefined,
        sczzrq: null,
        zzbx: [],
        jwbs: [2],
        lygj: undefined,
        lycs: undefined,
        lkdq: undefined,
        lyyn: undefined,
        field200: [],
        field201: [],
        field202: undefined,
        field203: null,
        field204: undefined,
        field205: undefined,
        field206: null,
        field207: undefined,
        field208: undefined,
        field209: undefined,
        field210: undefined,
        field211: undefined,
        field212: [],
        field213: [],
        field214: [],
        field215: [],
        field216: [],
        field217: [],
        field218: undefined,
        field219: [],
        field220: undefined,
        field221: [],
        field222: undefined,
        field223: [],
        field224: [],
        field225: undefined,
        field226: [],
        field227: undefined,
        field228: [],
        field229: undefined,
        field230: [],
        field231: [],
        field232: [],
        field233: undefined,
        field234: [],
        field235: undefined,
        field236: [],
        field237: undefined,
        field238: [],
        field239: undefined,
        field240: undefined,
        field241: undefined,
        field2411: '',
        field2412: '',
        field242: undefined,
        field243: undefined,
        field244: null,
        field245: [],
        field246: [],
        field247: []
      },
      rules: {
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
        country: [{
          required: true,
          message: '请选择国籍',
          trigger: 'change'
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
        field130: [{
          required: true,
          message: '请输入护照号码',
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
        }],
        field157: [{
          required: true,
          message: '请选择出入境时间',
          trigger: 'change'
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
        lxr: [{
          required: true,
          message: '请输入在华其他联系人',
          trigger: 'blur'
        }],
        lxrdh: [{
          required: true,
          message: '请输入联系人电话',
          trigger: 'blur'
        }],
        gafxqd: [{
          required: true,
          message: '个案发现渠道不能为空',
          trigger: 'change'
        }],
        twds: [{
          required: true,
          message: '请输入腋温测量最高  ',
          trigger: 'blur'
        }],
        sczzrq: [{
          required: true,
          message: '请选择首次症状日期',
          trigger: 'change'
        }],
        zzbx: [{
          required: true,
          type: 'array',
          message: '请至少选择一个症状',
          trigger: 'change'
        }],
        jwbs: [{
          required: true,
          type: 'array',
          message: '请至少选择一个既往病史',
          trigger: 'change'
        }],
        lygj: [{
          required: true,
          message: '请输入国家地区',
          trigger: 'blur'
        }],
        lycs: [{
          required: true,
          message: '请输入城市',
          trigger: 'blur'
        }],
        lkdq: [{
          required: true,
          message: '请输入离开地区',
          trigger: 'blur'
        }],
        lyyn: [{
          required: true,
          message: '请选择来自国家/地区是否流行同类症状的疾病',
          trigger: 'change'
        }],
        field200: [{
          required: true,
          type: 'array',
          message: '请至少选择一个发病前14天内 是 否 接触新型冠状病毒感染者或其密切接触者',
          trigger: 'change'
        }],
        field201: [{
          required: true,
          type: 'array',
          message: '请至少选择一个发病前14天内 是 否 接触有发热、干咳症状的人',
          trigger: 'change'
        }],
        field202: [{
          required: true,
          message: '请输入病人姓名',
          trigger: 'blur'
        }],
        field203: [{
          required: true,
          message: '请选择发病时间',
          trigger: 'change'
        }],
        field204: [{
          required: true,
          message: '请输入临床诊断',
          trigger: 'blur'
        }],
        field205: [{
          required: true,
          message: '请选择与本人关系',
          trigger: 'change'
        }],
        field206: [{
          required: true,
          message: '请选择最后接触时间',
          trigger: 'change'
        }],
        field207: [{
          required: true,
          message: '请选择接触方式',
          trigger: 'change'
        }],
        field208: [{
          required: true,
          message: '请选择接触频率',
          trigger: 'change'
        }],
        field209: [{
          required: true,
          message: '请选择接触地点',
          trigger: 'change'
        }],
        field210: [{
          required: true,
          message: '请输入与上面病人密切接触人员',
          trigger: 'blur'
        }],
        field211: [{
          required: true,
          message: '请输入共同暴露人员',
          trigger: 'blur'
        }],
        field212: [{
          required: true,
          type: 'array',
          message: '请至少选择一个病前14天内 是 否 去过酒吧、剧院、餐厅、医院、体育场馆、娱乐场所等公共场所',
          trigger: 'change'
        }],
        field213: [{
          required: true,
          type: 'array',
          message: '请至少选择一个发病前14天内 是 否 乘坐其他飞机、客（邮）轮、列车、地铁、客运汽车等公共交通工具',
          trigger: 'change'
        }],
        field214: [{
          required: true,
          type: 'array',
          message: '请至少选择一个发病前14天内 是 否 在公共室内环境下有效佩戴口罩，良好的手卫生习惯',
          trigger: 'change'
        }],
        field215: [{
          required: true,
          type: 'array',
          message: '请至少选择一个家庭、单位、旅行团等有 无2例及以上发热或呼吸道症状的病例',
          trigger: 'change'
        }],
        field216: [{
          required: true,
          type: 'array',
          message: '请至少选择一个来华（归国）的目的是 否与就医有关；',
          trigger: 'change'
        }],
        field217: [{
          required: true,
          type: 'array',
          message: '请至少选择一个发病前近14日内，是 否曾接受过新型冠状病毒检测',
          trigger: 'change'
        }],
        field218: [{
          required: true,
          message: '如接受过，则检测结果为不能为空',
          trigger: 'change'
        }],
        field219: [{
          required: true,
          type: 'array',
          message: '请至少选择一个发病前14天内 有 无野生动物、禽鸟类接触史',
          trigger: 'change'
        }],
        field220: [{
          required: true,
          message: '请输入具体接触情况',
          trigger: 'blur'
        }],
        field221: [{
          required: true,
          type: 'array',
          message: '请至少选择一个发病前14天内 有 无 感染环境暴露史？',
          trigger: 'change'
        }],
        field222: [{
          required: true,
          message: '请输入具体接触情况',
          trigger: 'blur'
        }],
        field223: [{
          required: true,
          type: 'array',
          message: '请至少选择一个有 无蚊虫叮咬史',
          trigger: 'change'
        }],
        field224: [{
          required: true,
          type: 'array',
          message: '请至少选择一个是 否从事动物饲养、宰杀、捕捉或标本制作工作',
          trigger: 'change'
        }],
        field225: [{
          required: true,
          message: '请输入具体接触情况',
          trigger: 'blur'
        }],
        field226: [{
          required: true,
          type: 'array',
          message: '请至少选择一个是 否从事病原生物学研究或医务工作',
          trigger: 'change'
        }],
        field227: [{
          required: true,
          message: '请输入具体接触情况',
          trigger: 'blur'
        }],
        field228: [{
          required: true,
          type: 'array',
          message: '请至少选择一个有无重点关注传染病预防接种史',
          trigger: 'change'
        }],
        field229: [{
          required: true,
          message: '请输入具体接种情况',
          trigger: 'blur'
        }],
        field230: [{
          required: true,
          type: 'array',
          message: '请至少选择一个有 无 怀孕',
          trigger: 'change'
        }],
        field231: [{
          required: true,
          type: 'array',
          message: '请至少选择一个有 无 晕机（车、船）史',
          trigger: 'change'
        }],
        field232: [{
          required: true,
          type: 'array',
          message: '请至少选择一个近期有 无 不详用药',
          trigger: 'change'
        }],
        field233: [{
          required: true,
          message: '请输入用药情况',
          trigger: 'blur'
        }],
        field234: [{
          required: true,
          type: 'array',
          message: '请至少选择一个是 否曾住院诊断',
          trigger: 'change'
        }],
        field235: [{
          required: true,
          message: '请输入诊断结果',
          trigger: 'blur'
        }],
        field236: [{
          required: true,
          type: 'array',
          message: '请至少选择一个近期有 无输血献血',
          trigger: 'change'
        }],
        field237: [{
          required: true,
          message: '请输入献血情况',
          trigger: 'blur'
        }],
        field238: [{
          required: true,
          type: 'array',
          message: '请至少选择一个有 无 过敏史',
          trigger: 'change'
        }],
        field239: [{
          required: true,
          message: '请输入过敏情形',
          trigger: 'blur'
        }],
        field240: [{
          required: true,
          message: '请输入其他相关因素调查',
          trigger: 'blur'
        }],
        field241: [{
          required: true,
          message: '初步判断及病例处理意见不能为空',
          trigger: 'change'
        }],
        field242: [{
          required: true,
          message: '流调人员签名',
          trigger: 'blur'
        }],
        field243: [{
          required: true,
          message: '带班人员签名',
          trigger: 'blur'
        }],
        field244: [{
          required: true,
          message: '请选择日期',
          trigger: 'change'
        }],
        field246: [{
          required: true,
          message: '请选择',
          trigger: 'change'
        }],
        field245: [{
          required: true,
          message: '请选择',
          trigger: 'change'
        }],
        field247: [{
          required: true,
          message: '请选择',
          trigger: 'change'
        }]
      },
      sfOptions: [{
        'label': '选项一',
        'value': 1
      }, {
        'label': '选项二',
        'value': 2
      }],
      Options: [{
        'label': '选项一',
        'value': 1
      }, {
        'label': '选项二',
        'value': 2
      }],
      xjdOptions: [{
        'label': '选项一',
        'value': 1
      }, {
        'label': '选项二',
        'value': 2
      }],
      gafxqdOptions: [{
        'label': '测温发现',
        'value': 1
      }, {
        'label': '交通工具负责人申报',
        'value': 2
      }, {
        'label': '医学巡查发现',
        'value': 3
      }, {
        'label': '个人申报',
        'value': 4
      }, {
        'label': '疫情通报',
        'value': 5
      }, {
        'label': '其他',
        'value': 6
      }],
      zzbxOptions: [{
        'label': '发热',
        'value': 99
      }, {
        'label': '乏力',
        'value': 1
      }, {
        'label': '干咳',
        'value': 2
      }, {
        'label': '鼻塞',
        'value': 3
      }, {
        'label': '流涕',
        'value': 4
      }, {
        'label': '咽痛',
        'value': 5
      }, {
        'label': '胃寒',
        'value': 6
      }, {
        'label': '寒战',
        'value': 7
      }, {
        'label': '气促',
        'value': 8
      }, {
        'label': '胸闷',
        'value': 9
      }, {
        'label': '呼吸困难',
        'value': 10
      }, {
        'label': '胸痛',
        'value': 11
      }, {
        'label': '咳血',
        'value': 12
      }, {
        'label': '呕吐',
        'value': 13
      }, {
        'label': '腹泻',
        'value': 14
      }, {
        'label': '腹痛',
        'value': 15
      }, {
        'label': '头痛',
        'value': 16
      }, {
        'label': '关节痛',
        'value': 17
      }, {
        'label': '肌肉痛',
        'value': 18
      }, {
        'label': '面色潮红',
        'value': 19
      }, {
        'label': '眼眶痛',
        'value': 20
      }, {
        'label': '黄疸',
        'value': 21
      }, {
        'label': '皮症',
        'value': 22
      }, {
        'label': '淋巴结肿大',
        'value': 23
      }, {
        'label': '淤血',
        'value': 24
      }, {
        'label': '颈项强直',
        'value': 25
      }, {
        'label': '盗汗',
        'value': 26
      }, {
        'label': '其他特异性症状',
        'value': 27
      }],
      jwbsOptions: [{
        'label': '肺部疾病（如哮喘、肺心病 、肺纤维化、矽肺等）',
        'value': 1
      }, {
        'label': '免疫缺陷类疾病',
        'value': 2
      }, {
        'label': '其他',
        'value': 3
      }],
      lyynOptions: [{
        'label': '是',
        'value': 1
      }, {
        'label': '否',
        'value': 2
      }],
      field200Options: [{
        'label': '是',
        'value': 1
      }, {
        'label': '否',
        'value': 2
      }],
      field201Options: [{
        'label': '是',
        'value': 1
      }, {
        'label': '否',
        'value': 2
      }],
      field246Options: [{
        'label': '是',
        'value': 1
      }, {
        'label': '否',
        'value': 2
      }],
      field245Options: [{
        'label': '是',
        'value': 1
      }, {
        'label': '否',
        'value': 2
      }],
      field205Options: [{
        'label': '家庭成员',
        'value': 1
      }, {
        'label': '同事',
        'value': 2
      }, {
        'label': '社会交往',
        'value': ''
      }, {
        'label': '共用交通工具',
        'value': ''
      }, {
        'label': '其他',
        'value': ''
      }],
      field207Options: [{
        'label': '与病人同进餐',
        'value': 1
      }, {
        'label': '与病人同处一室',
        'value': 2
      }, {
        'label': '与病人同一病区',
        'value': 3
      }, {
        'label': '与病人共用食具、茶具、毛巾、玩具等',
        'value': 4
      }, {
        'label': '接触病人分泌物、排泄物等',
        'value': 5
      }, {
        'label': '诊治护理',
        'value': 6
      }, {
        'label': '探视病人',
        'value': 7
      }, {
        'label': '其他接触',
        'value': 8
      }],
      field208Options: [{
        'label': '经常',
        'value': 6
      }, {
        'label': '有时',
        'value': 7
      }, {
        'label': '偶尔',
        'value': 8
      }],
      field209Options: [{
        'label': '家',
        'value': 6
      }, {
        'label': '工作单位',
        'value': 7
      }, {
        'label': '学校',
        'value': 8
      }, {
        'label': '集体宿舍',
        'value': ''
      }, {
        'label': '医院',
        'value': ''
      }, {
        'label': '室内公共场所',
        'value': ''
      }, {
        'label': '其他',
        'value': ''
      }],
      field212Options: [{
        'label': '是',
        'value': 1
      }, {
        'label': '否',
        'value': 2
      }],
      field213Options: [{
        'label': '是',
        'value': 1
      }, {
        'label': '否',
        'value': 2
      }],
      field214Options: [{
        'label': '是',
        'value': 1
      }, {
        'label': '否',
        'value': 2
      }],
      field215Options: [{
        'label': '有',
        'value': 1
      }, {
        'label': '无',
        'value': 2
      }],
      field216Options: [{
        'label': '是',
        'value': 1
      }, {
        'label': '否',
        'value': 2
      }],
      field217Options: [{
        'label': '是',
        'value': 1
      }, {
        'label': '否',
        'value': 2
      }],
      field218Options: [{
        'label': '阳性',
        'value': 1
      }, {
        'label': '隐形',
        'value': 2
      }, {
        'label': '结果未知',
        'value': ''
      }],
      field219Options: [{
        'label': '有',
        'value': 1
      }, {
        'label': '无',
        'value': 2
      }],
      field221Options: [{
        'label': '有',
        'value': 1
      }, {
        'label': '无',
        'value': 2
      }],
      field223Options: [{
        'label': '有',
        'value': 1
      }, {
        'label': '无',
        'value': 2
      }],
      field224Options: [{
        'label': '是',
        'value': 1
      }, {
        'label': '否',
        'value': 2
      }],
      field226Options: [{
        'label': '是',
        'value': 1
      }, {
        'label': '否',
        'value': 2
      }],
      field228Options: [{
        'label': '有',
        'value': 1
      }, {
        'label': '无',
        'value': 2
      }],
      field230Options: [{
        'label': '有',
        'value': 1
      }, {
        'label': '无',
        'value': 2
      }],
      field231Options: [{
        'label': '有',
        'value': 1
      }, {
        'label': '无',
        'value': 2
      }],
      field232Options: [{
        'label': '有',
        'value': 1
      }, {
        'label': '无',
        'value': 2
      }],
      field234Options: [{
        'label': '是',
        'value': 1
      }, {
        'label': '否',
        'value': 2
      }],
      field236Options: [{
        'label': '有',
        'value': 1
      }, {
        'label': '无',
        'value': 2
      }],
      field238Options: [{
        'label': '有',
        'value': 1
      }, {
        'label': '无',
        'value': 2
      }],
      field241Options: [{
        'label': '排除传染病可能，放行',
        'value': 1
      }, {
        'label': '不能排除新型冠状病毒肺炎，转送指定医疗机构诊治',
        'value': 2
      }, {
        'label': '按照呼吸道传播途径传染病进行排查和处置',
        'value': 3
      }, {
        'label': '按照消化道传播途径传染病进行排查和处置',
        'value': 4
      }, {
        'label': '按照蚊媒传播途径传染病进行排查和处置',
        'value': 5
      }],
      otherDesShow: false,
      countryOptions: [{
        'label': '中国',
        'value': 1
      }, {
        'label': '美国',
        'value': 2
      }],
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
    tableRowClassName({ row, rowIndex }) {
      if (rowIndex === 1) {
        return 'warning-row'
      } else if (rowIndex === 3) {
        return 'success-row'
      }
      return ''
    },
    handlerRow(row, column, evnet) {
      console.log(row.name)
      this.formData.field127 = row.name
      this.formData.country = 1
      this.formData.field128 = row.sex
      this.formData.field130 = row.zjhm
    },
    handlerRadio(value) {
      if (value === 6) {
        console.log(value)
        this.$set(this.zdjg, this.zdjg, true)
      }
    }
  }
}
</script>

<style scoped>

</style>
