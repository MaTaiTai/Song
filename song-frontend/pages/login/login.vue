<template>
	<view class="container">
		<view class="login-header">
			<text class="welcome-text">欢迎回来</text>
			<text class="sub-text">登录您的账户以继续点歌</text>
		</view>

		<view class="form-area">
			<view class="input-group">
				<text class="label">手机号/账号</text>
				<input class="input" type="text" placeholder="请输入手机号" placeholder-class="placeholder-style" v-model="username" />
			</view>
			<view class="input-group">
				<text class="label">密码</text>
				<input class="input" type="password" placeholder="请输入密码" placeholder-class="placeholder-style" v-model="password" />
			</view>

			<button class="btn-login" @click="handleLogin">登录</button>
			
			<view class="links">
				<text class="link-text" @click="goToSingerRegister">注册成为歌手</text>
				<text class="link-text">忘记密码?</text>
			</view>
		</view>
		
		<!-- Mock Admin Entry for demo -->
		<view class="debug-area" v-if="isAdmin">
			<button class="btn-admin" @click="goToAdmin">进入管理后台</button>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				username: '',
				password: '',
				isAdmin: false
			}
		},
		methods: {
			handleLogin() {
				// Mock login logic
				if (this.username === 'admin' && this.password === 'admin') {
					this.isAdmin = true;
					// Store admin session
					uni.setStorageSync('userRole', 'admin');
					uni.setStorageSync('isLoggedIn', true);
					
					uni.showToast({
						title: '管理员登录成功',
						icon: 'success'
					});
					setTimeout(() => {
						this.goToAdmin();
					}, 1000);
				} else if (this.username === 'singer' && this.password === 'singer') {
					// Store singer session
					uni.setStorageSync('userRole', 'singer');
					uni.setStorageSync('isLoggedIn', true);
					
					uni.showToast({
						title: '歌手登录成功',
						icon: 'success'
					});
					setTimeout(() => {
						uni.navigateTo({
							url: '/pages/singer/dashboard'
						});
					}, 1000);
				} else {
					uni.showToast({
						title: '登录成功',
						icon: 'success'
					});
				}
			},
			goToAdmin() {
				// Check session before navigating
				const role = uni.getStorageSync('userRole');
				if (role === 'admin') {
					uni.navigateTo({
						url: '/pages/admin/admin'
					});
				} else {
					uni.showToast({
						title: '请先登录管理员账号',
						icon: 'none'
					});
				}
			},
			goToSingerRegister() {
				uni.navigateTo({
					url: '/pages/singer/register'
				});
			}
		}
	}
</script>

<style>
	.container {
		padding: 40px 30px;
		background-color: #121212;
		min-height: 100vh;
		display: flex;
		flex-direction: column;
		justify-content: center;
	}

	.login-header {
		margin-bottom: 50px;
	}

	.welcome-text {
		font-size: 32px;
		font-weight: bold;
		color: #fff;
		display: block;
		margin-bottom: 10px;
	}

	.sub-text {
		font-size: 14px;
		color: #888;
	}

	.form-area {
		width: 100%;
	}

	.input-group {
		margin-bottom: 25px;
		background-color: #1E1E1E;
		padding: 15px 20px;
		border-radius: 15px;
		border: 1px solid #333;
	}

	.label {
		display: block;
		font-size: 12px;
		color: #888;
		margin-bottom: 5px;
	}

	.input {
		font-size: 16px;
		color: #fff;
		height: 24px;
		line-height: 24px;
	}

	.placeholder-style {
		color: #555;
	}

	.btn-login {
		margin-top: 40px;
		background: linear-gradient(45deg, #FFD700, #FFA500);
		color: #000;
		font-size: 16px;
		font-weight: bold;
		border-radius: 30px;
		height: 50px;
		line-height: 50px;
		box-shadow: 0 4px 15px rgba(255, 215, 0, 0.3);
	}
	
	.btn-login:active {
		opacity: 0.9;
		transform: scale(0.98);
	}

	.links {
		margin-top: 20px;
		display: flex;
		justify-content: space-between;
	}

	.link-text {
		font-size: 14px;
		color: #666;
	}
	
	.debug-area {
		margin-top: 30px;
		text-align: center;
	}
	
	.btn-admin {
		background-color: #333;
		color: #fff;
		font-size: 14px;
		border-radius: 20px;
	}
</style>
