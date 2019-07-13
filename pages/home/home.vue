<template>
	<view style="text-align: center;">
		您好  {{list.username}},欢迎回来!
	</view>
</template>

<script>
	var self;
	export default {
		data() {
			
			return {
				list: []
			}
		},
		onLoad() {
			//首先将实例指针保存到全局变量 self 方便在异步请求中访问实例本身
			self = this;
			uni.getStorage({
				key: 'userinfo',
				success: function(res) {
					const listdata = res.data;
					self.list = listdata;
					console.log("数据是:" + self.list.username)
				}
			});
		}
	}
</script>

<style>
	/* //首先将实例指针保存到全局变量 self 方便在异步请求中访问实例本身
			self=this;
			uni.getStorage({
				key:'userinfo',
				success: function(res) {
					const listdata=res.data;
					self.list=listdata;
					console.log("数据是:"+self.list[0]['username'])
				}
			}); */
</style>
