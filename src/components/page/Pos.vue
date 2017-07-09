<template>
  <div class="pos">
    <el-row>
    	<el-col :span="7" class="pos-order" id="order-list">
    		<el-tabs @tab-click="tabClick">
    			<el-tab-pane label="点餐" >
  					<el-table :data="tableData" border style="width:100%" max-height="300">
  						<el-table-column prop="goodsName" label="商品"></el-table-column>
  						<el-table-column prop="count" width="65" label="数量"></el-table-column>
  						<el-table-column prop="price" width="65" label="单价"></el-table-column>
  						<el-table-column  label="操作" width="100" fixed="right">
  							<template scope="scope">
  								<el-button type="text" size="small" @click="deleteOrderList(scope.$index,scope.row)">删除</el-button>
  								<el-button type="text" size="small" @click="addOrderList(scope.row)">增加</el-button>
  							</template>
  						</el-table-column>
  					</el-table>
            <div class="total">
              <span>数量: <strong>{{totalCount}}</strong></span>
              <span>金额: <strong>￥{{totalMoney}}</strong></span>
            </div>
  					<div class="bottom-div">
  						<el-button type="warning" size="small" @click="guadan">挂单</el-button>
  						<el-button type="danger" size="small" @click="deleteAllOrder">删除</el-button>		
  						<el-button type="success" size="small" @click="checkout">结账</el-button>		
  					</div>
    			</el-tab-pane>
	    		<el-tab-pane label="挂单" >
            <el-table :data="tableData" border style="width:100%" max-height="300">
              <el-table-column prop="goodsName" label="商品"></el-table-column>
              <el-table-column prop="count" width="65" label="数量"></el-table-column>
              <el-table-column prop="price" width="65" label="金额"></el-table-column>
              <el-table-column  label="操作" width="100" fixed="right">
                <template scope="scope">
                  <el-button type="text" size="small" @click="deleteOrderList(scope.$index,scope.row)">删除</el-button>
                  <el-button type="text" size="small" @click="addOrderList(scope.row)">增加</el-button>
                </template>
              </el-table-column>
            </el-table>
            <div class="total">
              <span>数量: <strong>{{totalCount}}</strong></span>
              <span>金额: <strong>￥{{totalMoney}}</strong></span>
            </div>
            <div class="bottom-div">
              <el-button type="danger" size="small" @click="deleteAllOrder">删除</el-button>    
              <el-button type="success" size="small" @click="checkout">结账</el-button>   
            </div>  
          </el-tab-pane>
	    		<el-tab-pane label="外卖">
            <el-table :data="tableData" border style="width:100%" max-height="300">
              <el-table-column prop="goodsName" label="商品"></el-table-column>
              <el-table-column prop="count" width="65" label="数量"></el-table-column>
              <el-table-column prop="price" width="65" label="金额"></el-table-column>
              <el-table-column  label="操作" width="100" fixed="right">
                <template scope="scope">
                  <el-button type="text" size="small" @click="deleteOrderList(scope.$index,scope.row)">删除</el-button>
                  <el-button type="text" size="small" @click="addOrderList(scope.row)">增加</el-button>
                </template>
              </el-table-column>
            </el-table>
            <div class="total">
              <span>数量: <strong>{{totalCount}}</strong></span>
              <span>金额: <strong>￥{{totalMoney}}</strong></span>
            </div>
            <div class="bottom-div">
              <el-button type="danger" size="small" @click="deleteAllOrder">删除</el-button>    
              <el-button type="success" size="small" @click="checkout">结账</el-button>   
            </div>   
          </el-tab-pane>
    		</el-tabs>
    	</el-col>
    	<el-col :span="17">
    		<div class="often-goods">
          <div class="title">常用商品</div>  
          <div class="often-goods-list">
            <ul>
              <li v-for="goods in oftenGoods" @click="addOrderList(goods)"><span>{{goods.goodsName}}</span><span class="oPrice">￥{{goods.price}}元</span></li>
            </ul>
          </div>
        </div>

        <div class="goods-type">
          <el-tabs>
            <el-tab-pane label="汉堡">
              <div>
                <ul class='cookList'>
                  <li v-for="goods in type0Goods" @click="addOrderList(goods)">
                      <span class="foodImg"><img :src="goods.goodsImg" width="100%"></span>
                      <span class="foodName">{{goods.goodsName}}</span>
                      <span class="foodPrice">￥{{goods.price}}元</span>
                  </li>
                </ul>
              </div>
            </el-tab-pane>
            <el-tab-pane label="小食">
              <div>
                <ul class='cookList'>
                  <li v-for="goods in type1Goods" @click="addOrderList(goods)">
                      <span class="foodImg"><img :src="goods.goodsImg" width="100%"></span>
                      <span class="foodName">{{goods.goodsName}}</span>
                      <span class="foodPrice">￥{{goods.price}}元</span>
                  </li>
                </ul>
              </div>
            </el-tab-pane>
            <el-tab-pane label="饮料">
              <div>
                <ul class='cookList'>
                  <li v-for="goods in type2Goods" @click="addOrderList(goods)">
                      <span class="foodImg"><img :src="goods.goodsImg" width="100%"></span>
                      <span class="foodName">{{goods.goodsName}}</span>
                      <span class="foodPrice">￥{{goods.price}}元</span>
                  </li>
                </ul>
              </div>
            </el-tab-pane>
            <el-tab-pane label="套餐">
              <div>
                <ul class='cookList'>
                  <li v-for="goods in type3Goods" @click="addOrderList(goods)">
                      <span class="foodImg"><img :src="goods.goodsImg" width="100%"></span>
                      <span class="foodName">{{goods.goodsName}}</span>
                      <span class="foodPrice">￥{{goods.price}}元</span>
                  </li>
                </ul>
              </div>
            </el-tab-pane>
          </el-tabs>
        </div>
    	</el-col>
    </el-row>
  </div>
    
</template>

<script>
import axios from 'axios' //哪里需要就在哪个文件中引入
export default {
  name: 'pos',
  mounted: function (){  //虚拟Dom 加载完执行
  	var orderHeight= document.body.clientHeight;
  	document.getElementById("order-list").style.height= orderHeight+"px";
  },
  data(){
  	return {
  		tableData:[],
      diancanData:[],
      guadanData:[],
      waimaiData:[],
      oftenGoods:[],
      type0Goods:[],
      type1Goods:[],
      type2Goods:[],
      type3Goods:[],
      totalCount:0,
      totalMoney:0,
      tabIndex:0
	   }
  },
  created:function (){
    axios.get('http://jspang.com/DemoApi/oftenGoods.php')
    .then(response=>{
      this.oftenGoods=response.data;
    })
    .catch(error=>{
      console.log(error);
      alert('网络错误，不能访问');
    });
    axios.get('http://jspang.com/DemoApi/typeGoods.php')
    .then(response=>{
      this.type0Goods=response.data[0];
      this.type1Goods=response.data[1];
      this.type2Goods=response.data[2];
      this.type3Goods=response.data[3];
    })
    .catch(error=>{
      console.log(error);
      alert('网络错误，不能访问');
    })
  },
  mounted: function (){
    var orderHeight = document.body.clientHeight;
    document.getElementById("order-list").style.height = orderHeight + "px"; 
  },
  methods:{
    addOrderList(goods){
      this.totalCount=0;
      this.totalMoney=0;
      //判断商品是否存在订单列表格局中
      let isHave = false;
      for (let i = 0; i < this.tableData.length; i++) {
        if(this.tableData[i].goodsId==goods.goodsId){
          isHave = true;
        }
      }
      //根据判断的值写逻辑
      if(isHave){
        //改变列表中商品的数量
        let arr=this.tableData.filter(o=>o.goodsId == goods.goodsId);
        arr[0].count++;
      }else{
        //新建这个商品的信息
        let newGoods = {goodsId:goods.goodsId,goodsName:goods.goodsName,price:goods.price,count:1};
        this.tableData.push(newGoods);
      }
      //计算汇总金额和数量
      this.calculateTotal();
    },
    deleteOrderList(index,goods){
      let arr=this.tableData.filter(o=>o.goodsId == goods.goodsId);
      arr[0].count--;
      if(arr[0].count<=0){
        this.tableData.splice(index,1);
      }
      //计算汇总金额和数量
      this.calculateTotal();
    },
    deleteAllOrder(){
      //删除所有商品
      this.tableData=[];
      this.totalCount=0;
      this.totalMoney=0;
    },
    calculateTotal(){
      //计算汇总金额和数量
      this.totalCount=0;
      this.totalMoney=0;
      if(this.tableData){
        this.tableData.forEach((element)=>{
          this.totalCount+=element.count;
          this.totalMoney+=element.price*element.count;
        })
      }
    },
    guadan(){
      //挂单,只能挂一单
      if(this.totalCount!=0){
        if(!this.guadanData.length){
          this.guadanData=this.noYinYong(this.tableData);
          this.tableData=[];
          this.totalCount=0;
          this.totalMoney=0;
          this.$message({
            message:"挂单成功！"
          })
        }else{
          this.$message({
            message:"已经挂了一单，不能同时挂两单！",
            type: 'warning'
          })
        }
      }else{
        this.$message({
          message:"请加入商品！",
          type: 'warning'
        })
      }
    },
    tabClick(tab, event){
      if(tab.index==0){
        this.goOrder();
      }else{
        if(tab.index==1){
          this.goGuadan();
        }else{
          this.goWaimai();
        }
      }
      this.tabIndex= tab.index;
    },
    storeData(){
      //储存当前tab页的数据
      if(this.tabIndex==0){
        this.diancanData= this.noYinYong(this.tableData);
      }else{
        if(this.tabIndex==1){
          this.guadanData= this.noYinYong(this.tableData);
        }else{
          this.waimaiData= this.noYinYong(this.tableData);
        }
      }
    },
    goOrder(){
      //去点单界面
      this.storeData();
      this.tableData= this.noYinYong(this.diancanData) //显示点餐页的数据
      this.calculateTotal();
    },
    goGuadan(){
      //去挂单界面
      this.storeData();
      this.tableData= this.noYinYong(this.guadanData); //显示挂单页的数据
      this.calculateTotal();
    },
    goWaimai(){
      //去外卖界面
      this.storeData();
      this.tableData= this.noYinYong(this.waimaiData); //显示外卖页的数据
      this.calculateTotal();
    },
    checkout(){
      if(this.totalCount!=0){
        this.tableData=[];
        this.totalCount=0;
        this.totalMoney=0;
        this.$message({
          message:"结账成功！",
          type: 'success'
        })
      }else{
        this.$message({
          message:"不能空结账！",
          type: 'warning'
        })
      }
    },
    noYinYong(arr){
      //解决对象引用传递问题
      let arrNew=[];
      for (let i = 0; i < arr.length; i++) {
        arrNew[i]={};
        for(let key in arr[i])arrNew[i][key]=arr[i][key];
      }
      return arrNew;
    }
  }
}
</script>


<style scoped>
.pos .pos-order{
	background: #f9fcfa;
	border-right: 1px solid #c0ccda;
}
.total{
  margin:20px auto;
  width: 100%;
  height: 30px; 
  line-height: 30px;
}
.total span{
  padding: 0 10px;
}
.title{
  height: 20px;
  padding: 10px;
  border-bottom: 1px solid #d3dce6;
  background: #f9fafc;
  text-align: left;
}
.often-goods-list ul li{
  list-style: none;
  float: left;
  margin: 10px;
  padding: 10px;
  border: 1px solid #f9fafc;
  background: #fff;
  cursor: pointer;
}
.oPrice{
  color: #58b7ff;
}
.goods-type{
  clear: both;
}
.cookList li{
   list-style: none;
   width:23%;
   border:1px solid #E5E9F2;
   height: auot;
   overflow: hidden;
   background-color:#fff;
   padding: 2px;
   float:left;
   margin: 2px;
  cursor: pointer;

}
.cookList li span{
   
    display: block;
    float:left;
}
.foodImg{
   width: 40%;
}
.foodName{
   font-size: 18px;
   padding-left: 10px;
   color:brown;

}
.foodPrice{
   font-size: 16px;
   padding-left: 10px;
   padding-top:10px;
}
</style>
