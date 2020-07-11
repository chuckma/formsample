<template>
  <div>

    <el-card class="box-card" style="margin:0 auto;width: 794px;height: 1123px">
      <div slot="header" class="clearfix" style="text-align: center;font-size: 22px">
        <span>出入境新型冠状病毒感染的肺炎染疫嫌疑人/染疫人情况报告</span>
      </div>
<!--      <el-row>-->
<!--&lt;!&ndash;        <el-form-item label="2312323" prop="field117">&ndash;&gt;-->
<!--&lt;!&ndash;          <el-input v-model="formData.field117" placeholder="海关" clearable :style="{width: '100%'}" />&ndash;&gt;-->
<!--&lt;!&ndash;        </el-form-item>&ndash;&gt;-->
<!--        <el-col>-->
<!--        <el-input v-model="formData.field117" placeholder="请输入海关名称" style="width: 300px;" class="el-input__inner">-->
<!--&lt;!&ndash;          <template slot="append">海关</template>&ndash;&gt;-->
<!--        </el-input>-->
<!--        </el-col>-->
<!--        <el-col>-->
<!--          <template><span>海关</span></template>-->
<!--        </el-col>-->

<!--      </el-row>-->

    <el-row>
      <h4 class="p-indent">XX海关关于报送在XX口岸检疫发现X例入/出境XXX病例有关情况的函</h4>
      <p class="p-indent">XXXX司：</p>
      <p class="p-indent"> XX年XX月XX日，XX海关在XX口岸检疫发现X例来自XXX的XXX病例，现将有关情况报送如下：</p>
      <p class="p-indent">一、病例概况</p>
      <p class="p-indent">
        病例姓名xxx，男/女，xx岁，xx国籍（护照号xxxxxx），职业xxx，居住地：xxxxxx（详细到具体小区和门牌号），联系电话：xxxxxx（国内可联系到的手机号码）。该病例近4周国际旅行史（详细到由具体时间点、旅行地点及旅行目的组成的旅行时间链，如x年x月x日从xx地到xx地做什么），xx月xx日乘机/船/车（班次、座位号）回国，经xx口岸入/出境。通过xx方式发现（如体温监测发现，应注明监测温度）。入/出境时水银体温计检测腋下体温xx.x℃，其他阳性症状和体征，蚊虫叮咬史、病人接触史、就诊用药史等。</p>
      <p class="p-indent">二、现场处置情况</p>
      <div  id="funitem">
        <ul>
          <li>（一）对该病例采取的检疫措施（如采样送检，转送指定传染病医院。或采样送检，给予健康建议、个人防护，发放就诊方便卡，嘱咐尽快就医诊治后放行）。
          </li>
          <li> （二）对该病例密切接触者进行了流行病学调查、医学检查和详细信息登记后放行。</li>
          <li> （三）将相关信息报送“智慧卫生检疫系统”（档案号xxxxx）。</li>
          <li> （四）对可能被污染的通道、场所、设施等实施消毒处理。</li>
        </ul>
      </div>
      <p class="p-indent">三、后续处置情况
      </p>
      <p class="p-indent">xx日，我关收到实验室（或地方医院）反馈，该名病例检测结果为xxx阳性。
        <p class="p-indent">        接到实验室反馈结果后，我关第一时间联系了该旅客，通知其实验室检测结果，了解其相关情况（目前停留具体地址、健康状况、就诊情况等），并要求尽快就诊做进一步诊治。</p>

      <p class="p-indent">特此致函。</p>

      <div >
<!--        <p style="float: right;margin-right: 20px; ">xx海关</p>-->
        <span style="display: block;position: relative;right: -620px;">xxx海关</span>
      </div>

      <div style="margin-top: 20px">
<!--        <span style="display: block;">201x年xx月xx日</span>-->
        <span style="display: block;position: relative;right: -600px;">201x年xx月xx日</span>

        <!--        <p style="">201x年xx月xx日</p>-->
      </div>
      <div>
        <div>
      <p class="p-indent">联系人：xxx，手机号码：xxxxxx</p>
        </div>

      </div>

    </el-row>
    </el-card>
  </div>
</template>

<script>
export default {
  name: 'Index',
  data() {
    return {
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
      }
    }
  }
}
</script>

<style scoped>
  .ss {
    border: 1px solid #ff0000;
    margin: 10px auto;
  }
  .ooel-input__inner{
    height: 30px;
  }
  .p-indent {
    text-indent: 2em;
  }

  #funitem ul li{
    list-style: none;
  }
</style>
