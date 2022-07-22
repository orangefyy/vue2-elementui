<template>
  <div>
    <el-container style="height: 100vh; border: 1px solid #eee">
      <el-aside width="40vw" style="background-color: rgb(238, 241, 246)">
        <div style="overflow-y: hidden; overflow-x: hidden">
          <h1 style="text-align: center; margin-bottom: 30px">
            个人信息登记表
          </h1>
          <el-form
            :model="dataForm"
            ref="dataForm"
            label-width="100px"
            class="demo-ruleForm"
            label-position="top"
          >
            <el-row>
              <el-col :span="6"
                ><div class="grid-content bg-purple-dark imgs">
                  <img v-if="dataForm.imgUrl" :src="dataForm.imgUrl" />
                  <div class="showurl" v-else></div>
                  <div>
                    <el-upload
                      class="upload-demo"
                      action="#"
                      :http-request="change"
                      :show-file-list="false"
                      multiple
                      :limit="3"
                      :file-list="dataForm.fileList"
                    >
                      <el-button size="mini">上传</el-button>
                      <el-button size="mini">更改</el-button>
                    </el-upload>
                  </div>
                </div></el-col
              >
              <el-col :span="18"
                ><div class="grid-content bg-purple-dark">
                  <h1>一 基本信息</h1>
                  <div
                    style="
                      display: flex;
                      justify-content: space-between;
                      width: 70%;
                    "
                  >
                    <el-form-item label="姓名" style="width: 40%">
                      <el-input v-model="dataForm.name"></el-input>
                    </el-form-item>
                    <el-form-item label="性别" style="width: 40%">
                      <el-radio v-model="dataForm.sex" label="1">男</el-radio>
                      <el-radio v-model="dataForm.sex" label="2">女</el-radio>
                    </el-form-item>
                  </div>
                  <div
                    style="
                      width: 70%;
                      display: flex;
                      justify-content: space-between;
                    "
                  >
                    <el-form-item label="出生年月">
                      <el-date-picker
                        v-model="dataForm.birthTime"
                        type="date"
                        style="width: 68%"
                        placeholder="选择日期"
                        value-format="yyyy-MM-dd"
                      >
                      </el-date-picker>
                    </el-form-item>
                    <el-form-item label="民族" style="width: 40%">
                      <el-input v-model="dataForm.typeEthnic"></el-input>
                    </el-form-item>
                  </div></div
              ></el-col>
              <div style="display: flex; width: 100%; padding: 0 20px">
                <el-form-item
                  label="政治面貌"
                  style="width: 18%; margin-right: 27px"
                >
                  <el-select
                    v-model="dataForm.typePoliticalvalue"
                    placeholder=""
                  >
                    <el-option
                      v-for="item in dataForm.typePolitical"
                      :key="item.value"
                      :label="item.label"
                      :value="item.value"
                    >
                    </el-option>
                  </el-select>
                </el-form-item>
                <div
                  style="
                    display: flex;
                    width: 54%;
                    justify-content: space-between;
                  "
                >
                  <el-form-item label="身份证号" style="width: 40%">
                    <el-input v-model="dataForm.identityNo"></el-input>
                  </el-form-item>
                  <el-form-item label="社保号" style="width: 40%">
                    <el-input v-model="dataForm.socialNo"></el-input>
                  </el-form-item>
                </div>
              </div>
              <div style="display: flex; width: 100%; padding: 0 20px">
                <el-form-item
                  label="手机"
                  style="width: 18%; margin-right: 27px"
                >
                  <el-input v-model="dataForm.phone"></el-input>
                </el-form-item>
                <div
                  style="
                    display: flex;
                    width: 54%;
                    justify-content: space-between;
                  "
                >
                  <el-form-item label="电子邮件" style="width: 40%">
                    <el-input v-model="dataForm.email"></el-input>
                  </el-form-item>
                  <el-form-item label="固定电话" style="width: 40%">
                    <el-input v-model="dataForm.tel"></el-input>
                  </el-form-item>
                </div>
              </div>
              <div style="display: flex; width: 100%; padding: 0 20px">
                <el-form-item
                  label="开户行名称"
                  style="width: 18%; margin-right: 27px"
                >
                  <el-input v-model="dataForm.bankname"></el-input>
                </el-form-item>
                <el-form-item label="" style="width: 54%">
                  <span
                    style="display: block; margin-bottom: 10px; font-size: 14px"
                    >银行卡号
                    <strong style="color: red"
                      >（非杭州联合开发银行不填）</strong
                    ></span
                  >
                  <el-input v-model="dataForm.account"></el-input>
                </el-form-item>
              </div>
              <div
                style="
                  display: flex;
                  width: 76%;
                  justify-content: space-between;
                  padding: 0 20px;
                "
              >
                <el-form-item label="联系地址" style="width: 57%">
                  <el-input v-model="dataForm.address"></el-input>
                </el-form-item>
                <el-form-item label="婚姻" style="width: 30%">
                  <el-select
                    v-model="dataForm.stateMarriagevalue"
                    placeholder=""
                  >
                    <el-option
                      v-for="item in dataForm.stateMarriage"
                      :key="item.value"
                      :label="item.label"
                      :value="item.value"
                    >
                    </el-option>
                  </el-select>
                </el-form-item>
              </div>
              <div
                style="
                  display: flex;
                  width: 76%;
                  justify-content: space-between;
                  padding: 0 20px;
                "
              >
                <el-form-item label="籍贯" style="width: 57%">
                  <el-input v-model="dataForm.nativePlace"></el-input>
                </el-form-item>
                <el-form-item label="邮编" style="width: 30%">
                  <el-input v-model="dataForm.postcode"></el-input>
                </el-form-item>
              </div>
              <div
                style="
                  display: flex;
                  width: 76%;
                  justify-content: space-between;
                  padding: 0 20px;
                "
              >
                <el-form-item label="户口" style="width: 57%">
                  <el-input v-model="dataForm.identityAddress"></el-input>
                </el-form-item>
                <el-form-item label="血型" style="width: 30%">
                  <el-input v-model="dataForm.typeBlood"></el-input>
                </el-form-item>
              </div>
            </el-row>
          </el-form>
        </div>
      </el-aside>

      <el-container width="40vw" style="padding: 0 20px; overflow-y: auto">
        <el-form
          label-position="top"
          label-width="80px"
          :model="formRight"
          ref="formRight"
        >
          <h1 style="margin-bottom: 20px">二 学业与技能信息</h1>
          <div style="display: flex; justify-content: space-between">
            <el-form-item label="毕业院校" style="width: 20%">
              <el-input v-model="formRight.graduatedSchool"></el-input>
            </el-form-item>
            <el-form-item label="学历" style="width: 20%">
              <el-input v-model="formRight.education"></el-input>
            </el-form-item>
            <el-form-item label="专业" style="width: 20%">
              <el-input v-model="formRight.profession"></el-input>
            </el-form-item>
            <el-form-item label="职称" style="width: 20%">
              <el-input v-model="formRight.jobTitle"></el-input>
            </el-form-item>
          </div>
          <div style="display: flex; justify-content: space-between">
            <el-form-item label="外语水平" style="width: 20%">
              <el-input v-model="formRight.foreignLanguageLevel"></el-input>
            </el-form-item>
            <el-form-item label="计算机水平" style="width: 20%">
              <el-input v-model="formRight.computerSkillLevel"></el-input>
            </el-form-item>
            <el-form-item label="特长" style="width: 47%">
              <el-input v-model="formRight.specialty"></el-input>
            </el-form-item>
          </div>
          <h1 style="margin-bottom: 20px">三 面试信息</h1>
          <div style="display: flex; justify-content: space-between">
            <el-form-item label="面试部门" style="width: 20%">
              <el-input v-model="formRight.interviewDepartment"></el-input>
            </el-form-item>
            <el-form-item label="面试岗位" style="width: 20%">
              <el-input v-model="formRight.interviewJob"></el-input>
            </el-form-item>

            <el-form-item label="报到时间" style="width: 47%">
              <el-date-picker
                v-model="dataForm.dateWork"
                type="date"
                style="width: 100%"
                placeholder=""
                value-format="yyyy-MM-dd"
              >
              </el-date-picker>
            </el-form-item>
          </div>
          <h1 style="margin-bottom: 20px">四 紧急联系人</h1>
          <el-table :data="tableData" border style="width: 100%">
            <el-table-column fixed prop="date" label="联系人" width="200">
              <template slot-scope="scope">
                <input
                  type="text"
                  v-model="scope.row.date"
                  style="
                    width: 100%;
                    height: 100%;
                    font-size: 20px;
                    border: none;
                    outline: none;
                  "
                />
                <!-- <span>{{scope.row.date}}</span> -->
              </template>
            </el-table-column>
            <el-table-column prop="relationship" label="与本人关系" width="330">
              <template slot-scope="scope">
                <input
                  type="text"
                  v-model="scope.row.relationship"
                  style="
                    width: 100%;
                    height: 100%;
                    font-size: 20px;
                    border: none;
                    outline: none;
                  "
                />
              </template>
            </el-table-column>
            <el-table-column prop="phone" label="联系方式" width="380">
              <template slot-scope="scope">
                <input
                  type="text"
                  v-model="scope.row.phone"
                  style="
                    width: 100%;
                    height: 100%;
                    font-size: 20px;
                    border: none;
                    outline: none;
                  "
                />
              </template>
            </el-table-column>
            <el-table-column prop="operation" label="操作" width="180">
              <template slot-scope="scope">
                <el-button
                  @click="Addrow()"
                  v-if="scope.$index == tableData.length - 1"
                  type="text"
                  size="small"
                  style="display: block; margin-left: 70px"
                >
                  新增
                </el-button>
                <el-button
                  v-else
                  @click.native.prevent="deleteRow(scope.$index)"
                  style="display: block; margin-left: 70px"
                  type="text"
                  size="small"
                >
                  删除
                </el-button>
              </template>
            </el-table-column>
          </el-table>
          <h1 style="margin: 20px 0">五 工作经历</h1>
          <el-table :data="tableDatatwo" border style="width: 100%">
            <el-table-column fixed prop="workDate " label="工作时间" width="120">
              <template slot-scope="scope">
                <input
                  type="text"
                  v-model="scope.row.workDate "
                  style="
                    width: 100%;
                    height: 100%;
                    font-size: 20px;
                    border: none;
                    outline: none;
                  "
                />
              </template>
            </el-table-column>
            <el-table-column prop="companyName " label="工作单位" width="120">
              <template slot-scope="scope">
                <input
                  type="text"
                  v-model="scope.row.companyName "
                  style="
                    width: 100%;
                    height: 100%;
                    font-size: 20px;
                    border: none;
                    outline: none;
                  "
                />
              </template>
            </el-table-column>
            <el-table-column prop="department " label="部门" width="170">
              <template slot-scope="scope">
                <input
                  type="text"
                  v-model="scope.row.department "
                  style="
                    width: 100%;
                    height: 100%;
                    font-size: 20px;
                    border: none;
                    outline: none;
                  "
                />
              </template>
            </el-table-column>
            <el-table-column prop="job " label="职务" width="120">
              <template slot-scope="scope">
                <input
                  type="text"
                  v-model="scope.row.job "
                  style="
                    width: 100%;
                    height: 100%;
                    font-size: 20px;
                    border: none;
                    outline: none;
                  "
                />
              </template>
            </el-table-column>
            <el-table-column prop="content " label="工作内容" width="380">
              <template slot-scope="scope">
                <input
                  type="text"
                  v-model="scope.row.content "
                  style="
                    width: 100%;
                    height: 100%;
                    font-size: 20px;
                    border: none;
                    outline: none;
                  "
                />
              </template>
            </el-table-column>
            <el-table-column prop="operation" label="操作" width="180">
              <template slot-scope="scope">
                <el-button
                  @click="Addrowtwo()"
                  v-if="scope.$index == tableDatatwo.length - 1"
                  type="text"
                  size="small"
                  style="display: block; margin-left: 70px"
                >
                  新增
                </el-button>
                <el-button
                  v-else
                  @click.native.prevent="
                    deleteRowtwo(scope.$index, tableDatatwo)
                  "
                  style="display: block; margin-left: 70px"
                  type="text"
                  size="small"
                >
                  删除
                </el-button>
              </template>
            </el-table-column>
          </el-table>
          <h1 style="margin: 20px 0">六 家庭状况</h1>
          <el-table :data="tableDatafive" border style="width: 100%">
            <el-table-column fixed prop="date" label="关系" width="120">
              <template slot-scope="scope">
                <input
                  type="text"
                  v-model="scope.row.date"
                  style="
                    width: 100%;
                    height: 100%;
                    font-size: 20px;
                    border: none;
                    outline: none;
                  "
                />
              </template>
            </el-table-column>
            <el-table-column prop="name" label="姓名" width="120">
              <template slot-scope="scope">
                <input
                  type="text"
                  v-model="scope.row.name"
                  style="
                    width: 100%;
                    height: 100%;
                    font-size: 20px;
                    border: none;
                    outline: none;
                  "
                />
              </template>
            </el-table-column>
            <el-table-column prop="phone" label="联系方式" width="170">
              <template slot-scope="scope">
                <input
                  type="text"
                  v-model="scope.row.phone"
                  style="
                    width: 100%;
                    height: 100%;
                    font-size: 20px;
                    border: none;
                    outline: none;
                  "
                />
              </template>
            </el-table-column>
            <el-table-column prop="companyName" label="工作单位" width="120">
              <template slot-scope="scope">
                <input
                  type="text"
                  v-model="scope.row.companyName"
                  style="
                    width: 100%;
                    height: 100%;
                    font-size: 20px;
                    border: none;
                    outline: none;
                  "
                />
              </template>
            </el-table-column>
            <el-table-column prop="address" label="家庭地址" width="380">
              <template slot-scope="scope">
                <input
                  type="text"
                  v-model="scope.row.address"
                  style="
                    width: 100%;
                    height: 100%;
                    font-size: 20px;
                    border: none;
                    outline: none;
                  "
                />
              </template>
            </el-table-column>
            <el-table-column prop="operation" label="操作" width="180">
              <template slot-scope="scope">
                <el-button
                  @click="Addrowfive()"
                  v-if="scope.$index == tableDatafive.length - 1"
                  type="text"
                  size="small"
                  style="display: block; margin-left: 70px"
                >
                  新增
                </el-button>
                <el-button
                  v-else
                  @click.native.prevent="
                    deleteRowfive(scope.$index, tableDatafive)
                  "
                  style="display: block; margin-left: 70px"
                  type="text"
                  size="small"
                >
                  删除
                </el-button>
              </template>
            </el-table-column>
          </el-table>
          <h1 style="margin: 20px 0">七 所获证书</h1>
          <el-table :data="tableDatathr" border style="width: 100%">
            <el-table-column
              fixed
              prop="certificateTypeId"
              label="证书名称"
              width="120"
            >
              <template slot-scope="scope">
                <input
                  type="text"
                  v-model="scope.row.certificateTypeId"
                  style="
                    width: 100%;
                    height: 100%;
                    font-size: 20px;
                    border: none;
                    outline: none;
                  "
                />
              </template>
            </el-table-column>
            <el-table-column prop="no " label="证书编号" width="120">
              <template slot-scope="scope">
                <input
                  type="text"
                  v-model="scope.row.no"
                  style="
                    width: 100%;
                    height: 100%;
                    font-size: 20px;
                    border: none;
                    outline: none;
                  "
                />
              </template>
            </el-table-column>
            <el-table-column prop="dateIssue " label="发证时间" width="170">
              <template slot-scope="scope">
                <input
                  type="text"
                  v-model="scope.row.dateIssue"
                  style="
                    width: 100%;
                    height: 100%;
                    font-size: 20px;
                    border: none;
                    outline: none;
                  "
                />
              </template>
            </el-table-column>
            <el-table-column prop="dateEffective " label="生效时间" width="120">
              <template slot-scope="scope">
                <input
                  type="text"
                  v-model="scope.row.dateEffective"
                  style="
                    width: 100%;
                    height: 100%;
                    font-size: 20px;
                    border: none;
                    outline: none;
                  "
                />
              </template>
            </el-table-column>
            <el-table-column prop="userName  " label="持证人" width="380">
              <template slot-scope="scope">
                <input
                  type="text"
                  v-model="scope.row.userName"
                  style="
                    width: 100%;
                    height: 100%;
                    font-size: 20px;
                    border: none;
                    outline: none;
                  "
                />
              </template>
            </el-table-column>
            <el-table-column prop="operation" label="操作" width="180">
              <template slot-scope="scope">
                <el-button
                  @click="Addrowthr()"
                  v-if="scope.$index == tableDatathr.length - 1"
                  type="text"
                  size="small"
                  style="display: block; margin-left: 70px"
                >
                  新增
                </el-button>
                <div
                  v-else
                  style="display: flex; justify-content: space-around"
                >
                  <el-button
                    type="text"
                    @click="handleClick(scope.row)"
                    size="small"
                    style="display: block"
                  >
                    预览
                  </el-button>
                  <el-button type="text" size="small" style="display: block">
                    下载
                  </el-button>
                  <el-button
                    @click.native.prevent="
                      deleteRowthr(scope.$index, tableDatathr)
                    "
                    style="display: block"
                    type="text"
                    size="small"
                  >
                    删除
                  </el-button>
                </div>
              </template>
            </el-table-column>
          </el-table>
          <h1 style="margin: 20px 0">八 添加附件</h1>
          <el-table :data="tableDatafour" border style="width: 100%">
            <el-table-column
              fixed
              prop="certificateTypeId"
              label="附件名称"
              width="260"
            >
              <template slot-scope="scope">
                <input
                  type="text"
                  v-model="scope.row.tableDatafour"
                  style="
                    width: 100%;
                    height: 100%;
                    font-size: 20px;
                    border: none;
                    outline: none;
                  "
                />
              </template>
            </el-table-column>
            <el-table-column prop="no " label="上传人" width="320">
              <template slot-scope="scope">
                <input
                  type="text"
                  v-model="scope.row.no"
                  style="
                    width: 100%;
                    height: 100%;
                    font-size: 20px;
                    border: none;
                    outline: none;
                  "
                />
              </template>
            </el-table-column>
            <el-table-column prop="dateIssue " label="上传时间" width="330">
              <template slot-scope="scope">
                <input
                  type="text"
                  v-model="scope.row.dateIssue"
                  style="
                    width: 100%;
                    height: 100%;
                    font-size: 20px;
                    border: none;
                    outline: none;
                  "
                />
              </template>
            </el-table-column>
            <el-table-column prop="operation" label="操作" width="180">
              <template slot-scope="scope">
                <el-button
                  @click="Addrowfour()"
                  v-if="scope.$index == tableDatafour.length - 1"
                  type="text"
                  size="small"
                  style="display: block; margin-left: 70px"
                >
                  新增
                </el-button>
                <div
                  v-else
                  style="display: flex; justify-content: space-around"
                >
                  <el-button
                    type="text"
                    @click="handleClick(scope.row)"
                    size="small"
                    style="display: block"
                  >
                    预览
                  </el-button>
                  <el-button type="text" size="small" style="display: block">
                    下载
                  </el-button>
                  <el-button
                    @click.native.prevent="
                      deleteRowfour(scope.$index, tableDatafour)
                    "
                    style="display: block"
                    type="text"
                    size="small"
                  >
                    删除
                  </el-button>
                </div>
              </template>
            </el-table-column>
          </el-table>
          <h1 style="margin: 20px 0">九 其它</h1>
          <div
            style="
              display: flex;
              flex-wrap: wrap;
              width: 100%;
              justify-content: space-between;
            "
          >
            <div>
              <p style="margin-bottom: 10px">1.奖惩情况</p>
              <el-input
                type="textarea"
                :rows="4"
                style="width: 500px"
                v-model="formRight.textarea"
              >
              </el-input>
            </div>
            <div>
              <p style="margin-bottom: 10px">2.个人学习计划</p>
              <el-input
                type="textarea"
                :rows="4"
                style="width: 500px"
                v-model="formRight.textareatwo"
              >
              </el-input>
            </div>
            <div>
              <p style="margin-bottom: 10px">3.培训情况</p>
              <el-input
                type="textarea"
                :rows="4"
                style="width: 500px"
                v-model="formRight.textareathr"
              >
              </el-input>
            </div>
            <div>
              <p style="margin-bottom: 10px">4.备注</p>
              <el-input
                type="textarea"
                :rows="4"
                style="width: 500px"
                v-model="formRight.textareafour"
              >
              </el-input>
            </div>
          </div>
          <el-button type="primary" @click="submit">立即创建</el-button>
        </el-form>
      </el-container>
    </el-container>
  </div>
</template>

<script>
export default {
  data() {
    return {
      dataForm: {
        imgUrl: "",
        name: "",
        sex: "1",
        birthTime: "",
        identityNo: "",
        typePolitical: [
          { value: 0, label: "群众" },
          { value: 1, label: "共青团员" },
          { value: 2, label: "中共党员" },
        ],
        nativePlace: "",
        typeEthnic: "",
        phone: "",
        tel: "",
        email: "",
        socialNo: "",
        stateMarriage: [
          { value: 0, label: "未婚" },
          { value: 1, label: "已婚" },
          { value: 2, label: "丧偶" },
          { value: 3, label: "离婚" },
        ],
        typePoliticalvalue: "",
        stateMarriagevalue: "",
        bankname: "",
        account: "",
        photo: "",
        address: "",
        typeBlood: "",
        identityAddress: "",
        postcode: "",
        fileList: [],
      },
      formRight: {
        graduatedSchool: "",
        education: "",
        profession: "",
        jobTitle: "",
        foreignLanguageLevel: "",
        computerSkillLevel: "",
        specialty: "",
        interviewDepartment: "",
        interviewJob: "",
        dateWork: "",
        textarea: "",
        textareatwo: "",
        textareathr: "",
        textareafour: "",
      },
      tableData: [{ date: "", relationship: "", phone: "" }, {}],
      tableDatatwo: [
        { workDate: "", companyName: "", department: "", job: "", content: "" },
        {},
      ],
      tableDatafive: [
        { date: "", name: "", phone: "", companyName: "", address: "" },
        {},
      ],
      tableDatathr: [
        {
          certificateTypeId: "",
          no: "",
          dateIssue: "",
          dateEffective: "",
          userName: "",
        },
        {},
      ],
      tableDatafour: [{ tableDatafour: "", no: "", dateIssue: "" }, {}],
    };
  },
  methods: {
    change(data) {
      console.log(data);
      let file = data.file;
      var reader = new FileReader();
      reader.readAsDataURL(file);
      reader.onload = () => {
        // console.log(this);
        // console.log(reader.result);
        this.dataForm.imgUrl = reader.result;
      };
      // console.log(fileList);
    },
    Form(formName) {
      this.$refs[formName].validate((valid) => {
        if (valid) {
          alert("submit!");
        } else {
          console.log("error submit!!");
          return false;
        }
      });
    },
    resetForm(formName) {
      this.$refs[formName].resetFields()``;
    },
    deleteRow(index) {
      // rows.splice(index, 1);
      this.tableData = this.tableData.filter((item, i) => {
        if (i != index) return item;
      });
    },
    Addrow() {
      this.tableData = [{}, ...this.tableData];
    },
    deleteRowtwo(index, rows) {
      rows.splice(index, 1);
    },
    Addrowtwo() {
      this.tableDatatwo = [{}, ...this.tableDatatwo];
    },
    deleteRowthr(index, rows) {
      rows.splice(index, 1);
    },
    Addrowthr() {
      this.tableDatathr = [{}, ...this.tableDatathr];
    },
    deleteRowfour(index, rows) {
      rows.splice(index, 1);
    },
    Addrowfour() {
      this.tableDatafour = [{}, ...this.tableDatafive];
    },
    deleteRowfive(index, rows) {
      rows.splice(index, 1);
    },
    Addrowfive() {
      this.tableDatafive = [{}, ...this.tableDatafive];
    },
    handleClick(row) {
      console.log(row);
    },
    submit() {
      if (!this.dataForm.name) {
        this.$message("请输入姓名!");
        return false;
      }
      if (!this.dataForm.sex) {
        this.$message("请输入性别!");
        return false;
      }
      if (!this.dataForm.birthTime) {
        this.$message("请输入出生日期!");
        return false;
      }
      if (!this.dataForm.identityNo) {
        this.$message("请输入身份证号!");
        return false;
      }
      if (!this.dataForm.socialNo) {
        this.$message("请输入社保号!");
        return false;
      }
      if (!this.dataForm.typePolitical) {
        this.$message("请输入政治面貌!");
        return false;
      }
      if (!this.dataForm.phone) {
        this.$message("请输入联系电话!");
        return false;
      }
      if (!this.dataForm.nativePlace) {
        this.$message("请输入籍贯!");
        return false;
      }
      if (!this.formRight.education) {
        this.$message("请输入学历!");
        return false;
      }
      if (!this.formRight.interviewDepartment) {
        this.$message("请输入面试部门!");
        return false;
      }
      if (!this.formRight.interviewJob) {
        this.$message("请输入面试岗位!");
        return false;
      }
      return true;
    },
  },
};
</script>
<style scoped>
.imgs {
  width: 80%;
  height: 160px;
  margin: 0 auto;
}
.imgs > img {
  width: 100%;
  height: 120px;
  border: 1px solid #ccc;
}
.imgs > .showurl {
  width: 80%;
  height: 160px;
  border: 1px solid #ccc;
  margin-bottom: 5px;
}
.el-button--mini,
.el-button--mini.is-round {
  padding: 7px 10px;
  margin: 20px 0px;
}
.el-dropdown-link {
  cursor: pointer;
  color: #409eff;
}
.el-icon-arrow-down {
  font-size: 12px;
}
.demonstration {
  display: block;
  color: #8492a6;
  font-size: 14px;
  margin-bottom: 20px;
}
.el-table > .cell {
  line-height: 23px;
}
</style>