<template>
  <div class="home">
      <form action="" id="myform">
          <div class="nav" >
              <p></p>
              <el-select v-model="value" placeholder="请选择仓库"  style="width:120px;">
                  <el-option v-for="item in ch" :key="item.value" :label="item.label" :value="item.value" id="one"></el-option>
              </el-select>
              <el-select v-model="value1" placeholder="请选择品种"  style="width:120px;">
                  <el-option v-for="item in pj" :key="item.value" :label="item.label" :value="item.value" id="two"></el-option>
              </el-select>
              <el-select v-model="value2" placeholder="请选择件数"  style="width:120px;">
                <el-option v-for="item in js" :key="item.value" :label="item.label" :value="item.value" id="three"></el-option>
              </el-select>
              <el-input v-model="input" placeholder="请填写净重" style="width:120px;"></el-input>
              <el-select v-model="value3" placeholder="请选择姓名"  style="width:120px;">
                  <el-option v-for="item in name" :key="item.value" :label="item.label" :value="item.value" id="four"></el-option>
              </el-select>
              <el-row>
              <el-button type="primary" size="small" style="height:30px;" @click="ck">出库</el-button>
              <el-button type="primary" size="small" style="height:30px;" @click="cz">重置</el-button>
              </el-row>
            </div>
            <div class="header">
                <el-checkbox v-model="checked">入库一览表</el-checkbox>
            </div>
            <div class="content" style="overflow:hidden;">
            <el-table  :data="tableData" border style="width: 100%;text-align:center;">
            <el-table-column fixed prop="date" label="时间" width="150"></el-table-column>
            <el-table-column prop="ch" label="仓库" width="150"></el-table-column>
            <el-table-column prop="ph" label="批号"  width="150"></el-table-column>
            <el-table-column prop="pj" label="品种" width="150"></el-table-column>
            <el-table-column prop="js" label="件数" width="150"></el-table-column>
            <el-table-column prop="jz" label="净重" width="150"></el-table-column>
            <el-table-column prop="name" label="姓名" width="150"></el-table-column>
            <el-table-column fixed="right" label="操作" width="140">
              <template v-slot="rowdata">
                <el-button type="primary" size="small" style="height:30px;" @click="bj(rowdata)">编辑</el-button>
              </template>
            </el-table-column>
            </el-table>
          </div>
          <div style="width:500px;height:400px;border:1px solid red;position:absolute;top:20%;left:40%;background-color:red;z-index:1;"></div>
                 <div class="block" style="display:flex;justify-content: space-between;">
                  <span class="demonstration"></span>
                   <el-pagination
                      @size-change="handleSizeChange"
                      @current-change="handleCurrentChange"
                      :current-page="currentPage4"
                      :page-sizes="[4, 5, 6, 7]"
                      :page-size="4"
                      layout="total, sizes, prev, pager, next, jumper"
                      :total="this.tableData.length">
                    </el-pagination>
                </div>
    </form> 
  </div>
</template>

<script>
// import HelloWorld from '@/components/HelloWorld.vue'

export default {
  name: 'home',
  components: {
    // HelloWorld
  },
  data(){
    return{
      checked: true,
      input:'',
      value:"",
      value1:"",
      value2:"",
      value3:"",
      currentPage4: 4,
       ch:[
            {value: 'A仓库',label: 'A仓库'}, 
            {value: 'B仓库',label: 'B仓库'}, 
            {value: 'C仓库',label: 'C仓库'},
            {value: 'D仓库',label: 'D仓库'}, 
            {value: 'E仓库',label: 'E仓库'}
         ],
        pj:[
            {value: '安卓',label: '安卓'}, 
            {value: '苹果',label: '苹果'}, 
        ],
        js:[
            {value: '500',label: '500'}, 
            {value: '1000',label: '1000'},
            {value: '2000',label: '2000'}, 
            {value: '5000',label: '5000'}, 
        ],
        name: [
            {value: '张三',label: '张三'}, 
            {value: '李四',label: '李四'}, 
            {value: '王五',label: '王五'}
         ],
         tableData: [
           {date: '2019-07-01',ch: 'A仓库',ph: '039-3816-1',pj: '安卓',js: '500',jz:'1000kg',name:'张三'},
           {date: '2019-07-01',ch: 'A仓库',ph: '039-3816-1',pj: '安卓',js: '500',jz:'1000kg',name:'张三'},
           {date: '2019-07-01',ch: 'A仓库',ph: '039-3816-1',pj: '安卓',js: '500',jz:'1000kg',name:'张三'},
      
         ]
     }
  },
  methods: {
      if(){

      }else {

      },
            
          // handleClick() { alert('button click');},
          cz:function(){
             document.getElementById("myform").reset();
          },
           ck:function(){
                        var date = new Date();
                        var seperator1 = "-";
                        var year = date.getFullYear();
                        var month = date.getMonth() + 1;
                        var strDate = date.getDate();
                        if (month >= 1 && month <= 9) {
                            month = "0" + month;
                        }
                        if (strDate >= 0 && strDate <= 9) {
                            strDate = "0" + strDate;
                        }
                        var currentdate = year + seperator1 + month + seperator1 + strDate;
                        var i=this.tableData.length+1;
                   this.tableData.push({
                    
                     date: currentdate,ch: this.value,ph:"039"+"-"+"3816"+"-"+i,pj: this.value1,js:this.value2,jz:this.input,name:this.value3
                   
                   });
                alert("出库成功！");
         },
          bj:function(data){
             var ch=data.row.ch;
             var ph=data.row.ph;
             var pj=data.row.pj;
             var js=data.row.js;
             var jz=data.row.jz;
             var name=data.row.name;
             var all=ch+ph+pj+js+jz+name;
             alert(all);
             alert(data.$index);
          },
            handleClick(row) {
              console.log(row);
            },
            handleSizeChange(val) {
              this.limitePage.limit = val;
            },
            handleCurrentChange(val) {
              this.limitePage.page = val
            }
         }
 }


</script>
<style lang="scss" scoped>

  *{padding:0px;margin:0px;font-family:"微软雅黑"}
  .home{
    width:1200px;margin:auto;
     .nav{width:100%;height:70px;border:1px solid #e4e4e4;margin-top:50px;
          display:flex;
          justify-content: space-around;
          line-height:70px; 
          .el-select-dropdown__item{
            background-color:#595454;
          }
     }
     .header{width:100%;height:50px;border:1px solid #e4e4e4;margin-top:30px;background-color:#f3f3f3;font-size:14px;
          label{
            margin-left:30px;
            line-height:50px;
            input{
              margin-left:20px;
            }
          }
     }
     .content{width:100%;height:300px;border:1px solid #e4e4e4;margin-top:30px;}
     
  }
 
</style>

