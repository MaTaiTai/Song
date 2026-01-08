<template>
	<view class="container">
		<view class="header">
			<text class="title">成为驻场歌手</text>
			<text class="subtitle">Join Us & Share Your Voice</text>
		</view>

		<view class="form-area">
			<view class="input-group">
				<text class="label">真实姓名</text>
				<input class="input" type="text" placeholder="请输入真实姓名" placeholder-class="placeholder-style" v-model="form.realName" />
			</view>
			
			<view class="input-group">
				<text class="label">艺名 (展示给观众)</text>
				<input class="input" type="text" placeholder="请输入艺名" placeholder-class="placeholder-style" v-model="form.stageName" />
			</view>
			
			<view class="row">
				<view class="input-group half">
					<text class="label">年龄</text>
					<input class="input" type="number" placeholder="年龄" placeholder-class="placeholder-style" v-model="form.age" />
				</view>
				<view class="input-group half">
					<text class="label">手机号</text>
					<input class="input" type="number" placeholder="手机号" placeholder-class="placeholder-style" v-model="form.phone" />
				</view>
			</view>

			<view class="input-group">
				<text class="label">邮箱</text>
				<input class="input" type="text" placeholder="请输入邮箱地址" placeholder-class="placeholder-style" v-model="form.email" />
			</view>
			
			<view class="input-group">
				<text class="label">设置密码</text>
				<input class="input" type="password" placeholder="设置登录密码" placeholder-class="placeholder-style" v-model="form.password" />
			</view>
			
			<view class="input-group">
				<text class="label">确认密码</text>
				<input class="input" type="password" placeholder="再次输入密码" placeholder-class="placeholder-style" v-model="form.confirmPassword" />
			</view>

			<button class="btn-submit" @click="handleSubmit">提交申请</button>
			<button class="btn-back" @click="goBack">返回登录</button>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				form: {
					realName: '',
					stageName: '',
					age: '',
					phone: '',
					email: '',
					password: '',
					confirmPassword: ''
				}
			}
		},
		methods: {
			handleSubmit() {
				// Basic validation
				if (!this.form.realName || !this.form.phone || !this.form.password) {
					uni.showToast({
						title: '请填写完整信息',
						icon: 'none'
					});
					return;
				}
				if (this.form.password !== this.form.confirmPassword) {
					uni.showToast({
						title: '两次密码不一致',
						icon: 'none'
					});
					return;
				}

				// Mock submission
				uni.showLoading({ title: '提交中...' });
				setTimeout(() => {
					uni.hideLoading();
					uni.showModal({
						title: '申请已提交',
						content: '您的驻场歌手申请已提交审核，我们会尽快通过短信通知您结果。',
						showCancel: false,
						success: () => {
							this.goBack();
						}
					});
				}, 1500);
			},
			goBack() {
				uni.navigateBack();
			}
		}
	}
</script>

<style>
	.container {
		padding: 30px;
		background-color: #121212;
		min-height: 100vh;
	}

	.header {
		margin-bottom: 30px;
		margin-top: 20px;
	}

	.title {
		font-size: 28px;
		font-weight: bold;
		color: #FFD700;
		display: block;
		margin-bottom: 5px;
	}

	.subtitle {
		font-size: 14px;
		color: #888;
		letter-spacing: 1px;
	}

	.form-area {
		width: 100%;
	}

	.input-group {
		margin-bottom: 20px;
		background-color: #1E1E1E;
		padding: 12px 15px;
		border-radius: 10px;
		border: 1px solid #333;
	}
	
	.row {
		display: flex;
		gap: 15px;
	}
	
	.half {
		flex: 1;
	}

	.label {
		display: block;
		font-size: 12px;
		color: #888;
		margin-bottom: 5px;
	}

	.input {
		font-size: 14px;
		color: #fff;
		height: 24px;
		line-height: 24px;
	}

	.placeholder-style {
		color: #555;
	}

	.btn-submit {
		margin-top: 30px;
		background: linear-gradient(45deg, #FFD700, #FFA500);
		color: #000;
		font-size: 16px;
		font-weight: bold;
		border-radius: 25px;
		height: 48px;
		line-height: 48px;
	}
	
	.btn-back {
		margin-top: 15px;
		background: transparent;
		color: #888;
		font-size: 14px;
		border: 1px solid #333;
		border-radius: 25px;
		height: 44px;
		line-height: 42px;
	}
	
	.btn-submit:active, .btn-back:active {
		opacity: 0.8;
	}
</style>
