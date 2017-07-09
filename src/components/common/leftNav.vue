<template>
	<div class="leftNav">
		<ul>
			<li>
				<i class="icon iconfont icon-goumai"></i>
				<div>收银</div>
			</li>
			<li>
				<i class="icon iconfont icon-dianpu"></i>
				<div>店铺</div>
			</li>
			<li>
				<i class="icon iconfont icon-hanbao"></i>
				<div>商品</div>
			</li>
			<li>
				<i class="icon iconfont icon-zuanshi"></i>
				<div>会员</div>
			</li>
			<li>
				<i class="icon iconfont icon-chanpincanshu"></i>
				<div>统计</div>
			</li>
			<li>
				<i class="icon iconfont icon-gongnengjianyi"></i>
				<div>设置</div>
			</li>

		</ul>
	</div>
</template>
<script>
	export default{

	}
</script>
<style>
.leftNav{
	float: left;
	width: 5%;
	color: #fff;
	font-size: 10px;
	height: 100%;
	background: #1d8ce0;
}
.iconfont{
	font-size:24px;
}
.leftNav ul{
	margin: 50px 0;
	padding: 0;
}
.leftNav ul li{
	padding: 10px 0;
	margin: 10px auto;
	list-style: none;
	text-align: center;
	cursor: pointer;
	border-bottom: 1px solid #20a0ff;
}
.leftNav ul li:hover{
	background: #d44;
}
</style>