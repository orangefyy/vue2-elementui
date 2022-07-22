<template>
  <div>
    <h1 style="text-align: center; margin-bottom: 30px">个人信息登记表</h1>
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
              style="display: flex; justify-content: space-between; width: 70%"
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
              style="width: 70%; display: flex; justify-content: space-between"
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
          <el-form-item label="政治面貌" style="width: 18%; margin-right: 27px">
            <el-select v-model="dataForm.typePoliticalvalue" placeholder="">
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
            style="display: flex; width: 54%; justify-content: space-between"
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
          <el-form-item label="手机" style="width: 18%; margin-right: 27px">
            <el-input v-model="dataForm.phone"></el-input>
          </el-form-item>
          <div
            style="display: flex; width: 54%; justify-content: space-between"
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
            <span style="display: block; margin-bottom: 10px; font-size: 14px"
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
            <el-select v-model="dataForm.stateMarriagevalue" placeholder="">
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
</template>
<script>
export default {
    data(){
        return{
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
        }
    },
    methods :{
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
      this.$refs[formName].resetFields();
    }
    }
}
</script>