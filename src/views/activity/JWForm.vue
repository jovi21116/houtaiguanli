<template>
  <el-form ref="form" :model="form" :rules="rules" label-width="80px" style="margin:20px;min-width:500px;max-width:800px;">
    <el-form-item label="活动名称" prop="name" class="name">
      <el-input v-model="form.name"></el-input>
    </el-form-item>
    <el-form-item label="活动区域" prop="region">
      <el-select v-model="form.region" placeholder="请选择活动区域">
        <el-option label="区域一" value="shanghai"></el-option>
        <el-option label="区域二" value="beijing"></el-option>
      </el-select>
    </el-form-item>
    <el-form-item label="活动时间" required>
      <el-col :span="11" class="datePicker">
        <el-form-item prop="date1">
        <el-date-picker type="date" placeholder="选择日期" v-model="form.date1" style="width: 100%;"></el-date-picker>
        </el-form-item>
      </el-col>
      <el-col :span="2" class="line">-</el-col>
      <el-col :span="11" class="datePicker">
        <el-form-item prop="date2">
        <el-time-picker type="fixed-time" placeholder="选择时间" v-model="form.date2" style="width: 100%;"></el-time-picker>
        </el-form-item>
      </el-col>
    </el-form-item>
    <el-form-item label="即时配送" prop="delivery">
      <el-switch v-model="form.delivery"></el-switch>
    </el-form-item>
    <el-form-item label="活动性质" prop="type">
      <el-checkbox-group v-model="form.type">
        <el-checkbox label="美食/餐厅线上活动" name="type"></el-checkbox>
        <el-checkbox label="地推活动" name="type"></el-checkbox>
        <el-checkbox label="线下主题活动" name="type"></el-checkbox>
        <el-checkbox label="单纯品牌曝光" name="type"></el-checkbox>
      </el-checkbox-group>
    </el-form-item>
    <el-form-item label="特殊资源" prop="resource">
      <el-radio-group v-model="form.resource">
        <el-radio label="线上品牌商赞助"></el-radio>
        <el-radio label="线下场地免费"></el-radio>
      </el-radio-group>
    </el-form-item>
    <el-form-item label="活动形式" prop="desc">
      <el-input type="textarea" v-model="form.desc"></el-input>
    </el-form-item>
    <el-form-item>
      <el-button type="primary" @click="createClick">立即创建</el-button>
      <el-button @click="cancel">取消</el-button>
    </el-form-item>
  </el-form>
</template>

<script>
export default {
  name: 'JWForm',
  data () {
    return {
      submit:false,
      form:{
        name: '',
        region: '',
        date1: '',
        date2: '',
        delivery: false,
        type: [],
        resource: '',
        desc: ''
      },
      rules:{
        name: [
          { required: true, message: '请输入活动名称', trigger: 'blur' },
          { min: 3, max: 5, message: '长度在 3 到 5 个字符', trigger: 'blur' }
        ],
        region: [
          { required: true, message: '请选择活动区域', trigger: 'change' }
        ],
        date1: [
          { type: 'date', required: true, message: '请选择日期', trigger: 'change' }
        ],
        date2: [
          { type: 'date', required: true, message: '请选择时间', trigger: 'change' }
        ],
        type: [
          { type: 'array', required: true, message: '请至少选择一个活动性质', trigger: 'change' }
        ],
        resource: [
          { required: true, message: '请选择活动资源', trigger: 'change' }
        ],
        desc: [
          { required: true, message: '请填写活动形式', trigger: 'blur' }
        ]
      }
    }
  },
  methods:{
    createClick(){
      this.$confirm("confirm?","tip",{}).then(() => {
        this.$message({
          message:"success",
          type:"success"
        }).catch(() => {

        });
        this.submit=true;
        this.$router.push({path:'/table'});
        
      });
    },
    cancel(){
      // this.$confirm("cancel?","tip",{}).then(() => {
        this.$router.push({path:'/table'});
      // });
    }
  },
  beforeRouteLeave(to,from,next){
    
    if(!this.submit){
      this.$confirm("cancel?","tip",{}).then(() => {
        next();
      }).catch(() => {
        
      });
    }else{
      next();
    }
    
  }

}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="scss" scoped>

.el-form {
  text-align: left;

  .name {
    width: 300px;
  }
  .datePicker {
    width:160px;
  }
  .line {
    text-align: center;
    width:30px;
  }
}


</style>