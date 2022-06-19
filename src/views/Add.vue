<template>
  <div>
    <el-form ref="form" :model="form" label-width="80px">
      <el-form-item label="商品名称">
        <el-input v-model="form.GoodsName"></el-input>
      </el-form-item>

      <el-form-item label="商品类别">
        <el-col :span="6">
          <el-select v-model="form.Type1Id" @change="changeTypeList(form.Type1Id)" placeholder="请选择类别">
            <el-option
              :label="item.TypeName"
              :key="item.Tid"
              v-for="item in Type1List"
              :value="item.Tid"
            ></el-option>
          </el-select>
        </el-col>
        
        <el-col :span="6">
          <el-select v-model="form.Type2Id" @change="changeTypeList2(form.Type2Id)"  placeholder="请选择类别">
            <el-option
              :label="item.TypeName"
              :key="item.Tid"
              v-for="item in Type2List"
              :value="item.Tid"
            ></el-option>
          </el-select>
        </el-col>

        <el-col :span="6">
          <el-select v-model="form.Type3Id" placeholder="请选择类别">
            <el-option
              :label="item.TypeName"
              :key="item.Tid"
              v-for="item in Type3List"
              :value="item.Tid"
            ></el-option>
          </el-select>
        </el-col>

      </el-form-item>
      <!-- <el-form-item label="活动时间">
        <el-col :span="11">
          <el-date-picker
            type="GoodsDate"
            placeholder="选择日期"
            v-model="form.date1"
            style="width: 100%"
          ></el-date-picker>
        </el-col>
      </el-form-item> -->
     
      <el-form-item label="活动性质">
        <el-checkbox-group v-model="form.GoodsImg">
          <el-checkbox label="美食/餐厅线上活动" name="type"></el-checkbox>
          <el-checkbox label="地推活动" name="type"></el-checkbox>
          <el-checkbox label="线下主题活动" name="type"></el-checkbox>
          <el-checkbox label="单纯品牌曝光" name="type"></el-checkbox>
        </el-checkbox-group>
      </el-form-item>
     
      <el-form-item>
        <el-button type="primary" @click="onSubmit">立即创建</el-button>
        <el-button>取消</el-button>
      </el-form-item>
    </el-form>
  </div>
</template>

<script>
export default {
  data() {
    return {
      form: {
        Type1Id: "",
        Type2Id: "",
        Type3Id: "",
        GoodsName: "",
        GoodsDate: "",
        GoodsImg: "",
      },
      Type1List: [],
      Type2List: [],
      Type3List: [],
    };
  },
  watch:{
    
  }
  ,
  methods: {
    onSubmit() {
      console.log("submit!");
    },
    changeTypeList(val){
      debugger;
      this.Type2List=[];
      this.form.Type2Id="";
      this.Type3List=[];
      this.form.Type3Id="";
        this.getTypeList(val,2);
    },
    changeTypeList2(val){
       this.Type3List=[];
       this.form.Type3Id="";
       this.getTypeList(val,3);
    },
    getTypeList(val,typeId){
      
        this.$axios.get("https://localhost:44369/api/Goods/GetGoodsType?id="+val).then(
            res=>{
                switch(typeId){
                  case 1:
                    this.Type1List=res.data;
                    break;
                    case 2:
                      this.Type2List=res.data;
                    break;
                    case 3:
                      this.Type3List=res.data;
                    break;
                }
            }
        )
    },
  },
  created(){
    this.getTypeList(1,1);
  }
};
</script>
