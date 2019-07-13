<template>
	<view class="content">
		<view class="row">
			<text class="title">用户名:</text>
			<input v-model="username" type="text" placeholder="请输入用户名" />
		</view>

		<view class="row">
			<view class="title">密 码:</view>
			<input v-model="pwd" type="text" placeholder="请输入密码" />
		</view>
		<view class="btg">
			<button type="primary" @tap="btn">登录</button>
		</view>

	</view>
</template>

<script>
	var self;
	export default {
		data() {
			lists:[],
			self=this
			return {
				// list:[],
				username: '',
				pwd: ''
			}
		},
		methods: {
			btn() {
				if (this.username.length <= 0) {
					uni.showToast({
						icon: 'none',
						title: '请输入用户名'
					});
					return;
				}
				if (this.pwd.length <= 0) {
					uni.showToast({
						icon: 'none',
						title: '请输入密码'
					});
					return;
				}
		
				uni.request({
					url: 'http://192.168.250.129:8080/login', //仅为示例，并非真实接口地址。
					method:'POST',
					header:{
						'content-type':'application/json',
					},
					data: {
						username: this.username,
						password: this.pwd
					},success: (res) => {
						
						let list=res.data;
						console.log("返回数据状态:" + list);
						console.log(list.code);
						if(list.code !="200"){
							uni.showToast({
								icon: 'none',
								title: '用户名或密码错误'
							});
							return;
						}
						const data=res.data;
						self.lists=data;
						// console.log("返回数据状态:" + JSON.stringify(res));
						
						// console.log("返回数据状态:" + self.lists[0]['rolename']);
						
						// uni.setStorage({
						// 	key:'userinfo',
						// 	data:{
						// 		bh:self.lists[0]['bh'],
						// 		rolename:self.lists[0]['rolename'],
						// 		username:self.lists[0]['username']
						// 		
						// 	}
						// })
                        // console.log("返回数据状态:" +list[8]);
						
						
						//解析数据
						uni.showToast({
							icon: 'none',
							title: '登录成功'
						});
						
						var demo =list.data;
						console.log(demo);
						
						uni.navigateTo({
							url: '../home/home',
						});
						
					},fail: () => {
						uni.showToast({
							icon: 'none',
							title: '网络异常,请稍后重试'
						});
					}


				});

				


				// 				uni.showToast({
				// 					icon: 'none',
				// 					title: this.username+'-----'+this.pwd
				// 				});
				// 
				// 				if (this.username==123 && this.pwd==123) {
				// 					uni.showToast({
				// 						title: '登录成功'
				// 					});
// 									uni.navigateTo({
// 										url: '../index/index',
// 									});
				// 
				// 				} else {
				// 					uni.showToast({
				// 						icon: 'none',
				// 						title: '用户名或密码错误'
				// 					});
				// 				}


			},
		}
	}
</script>

<style>
	.content {
		min-height: 100%;
		flex: 1;
		flex-direction: column;
		background-color: #efeff4;
		padding: 20px;
	}

	.btg {
		margin-top: 10px;
	}

	.row {
		margin-top: 10px;
		display: flex;
		flex-direction: row;
		position: relative;
		background-color: #ffffff;
	}

	.group {
		background-color: #ffffff;
		position: relative;
	}

	.row input {
		width: 80%;
		height: 25px;
		min-height: 25px;
		padding: 15px 0;
		padding-right: 30px;
		line-height: 25px;
	}

	.row .title {
		width: 30%;
		height: 25px;
		min-height: 25px;
		padding: 15px 0;
		padding-left: 30px;
		line-height: 25px;
	}

	.group {
		background-color: #ffffff;
		margin-top: 40px;
		position: relative;
	}
</style>
