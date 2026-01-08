<template>
	<view class="container">
		<view class="header">
			<text class="title">歌手审核</text>
			<text class="subtitle">Pending Applications</text>
		</view>

		<view class="tabs">
			<view class="tab-item active">待审核 ({{pendingList.length}})</view>
			<view class="tab-item">已审核</view>
		</view>

		<view class="audit-list">
			<view class="audit-card" v-for="(item, index) in pendingList" :key="index">
				<view class="card-header">
					<view class="user-info">
						<text class="user-name">{{item.realName}}</text>
						<text class="user-meta">申请艺名: {{item.stageName}}</text>
					</view>
					<text class="time">{{item.time}}</text>
				</view>
				
				<view class="card-body">
					<view class="info-row">
						<text class="label">手机号:</text>
						<text class="value">{{item.phone}}</text>
					</view>
					<view class="info-row">
						<text class="label">年龄:</text>
						<text class="value">{{item.age}}</text>
					</view>
					<view class="info-row">
						<text class="label">邮箱:</text>
						<text class="value">{{item.email}}</text>
					</view>
				</view>
				
				<view class="card-footer">
					<button class="btn btn-reject" @click="handleReject(index)">拒绝</button>
					<button class="btn btn-approve" @click="handleApprove(index)">通过</button>
				</view>
			</view>
			
			<view v-if="pendingList.length === 0" class="empty-state">
				<text>暂无待审核申请</text>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				pendingList: [
					{
						realName: '李明',
						stageName: 'Leon',
						phone: '13800138000',
						age: 24,
						email: 'leon@example.com',
						time: '10分钟前'
					},
					{
						realName: '王芳',
						stageName: 'Angel',
						phone: '13900139000',
						age: 22,
						email: 'angel@example.com',
						time: '2小时前'
					}
				]
			}
		},
		methods: {
			handleApprove(index) {
				uni.showModal({
					title: '确认通过',
					content: `确定要通过 ${this.pendingList[index].stageName} 的歌手申请吗？`,
					success: (res) => {
						if (res.confirm) {
							uni.showToast({
								title: '已通过审核',
								icon: 'success'
							});
							this.pendingList.splice(index, 1);
						}
					}
				});
			},
			handleReject(index) {
				uni.showModal({
					title: '确认拒绝',
					content: '请输入拒绝理由',
					editable: true,
					placeholderText: '如：信息填写不完整',
					success: (res) => {
						if (res.confirm) {
							uni.showToast({
								title: '已拒绝申请',
								icon: 'none'
							});
							this.pendingList.splice(index, 1);
						}
					}
				});
			}
		}
	}
</script>

<style>
	.container {
		padding: 20px;
		background-color: #121212;
		min-height: 100vh;
	}

	.header {
		margin-bottom: 20px;
	}

	.title {
		font-size: 24px;
		font-weight: bold;
		color: #fff;
		display: block;
	}

	.subtitle {
		font-size: 12px;
		color: #666;
	}
	
	.tabs {
		display: flex;
		border-bottom: 1px solid #333;
		margin-bottom: 20px;
	}
	
	.tab-item {
		padding: 10px 20px;
		color: #888;
		font-size: 14px;
		position: relative;
	}
	
	.tab-item.active {
		color: #FFD700;
		font-weight: bold;
	}
	
	.tab-item.active::after {
		content: '';
		position: absolute;
		bottom: -1px;
		left: 20px;
		right: 20px;
		height: 2px;
		background-color: #FFD700;
	}

	.audit-card {
		background-color: #1E1E1E;
		border-radius: 12px;
		padding: 20px;
		margin-bottom: 15px;
		border: 1px solid #333;
	}

	.card-header {
		display: flex;
		justify-content: space-between;
		align-items: flex-start;
		margin-bottom: 15px;
		padding-bottom: 15px;
		border-bottom: 1px solid #2a2a2a;
	}

	.user-name {
		font-size: 16px;
		font-weight: bold;
		color: #fff;
		display: block;
		margin-bottom: 4px;
	}

	.user-meta {
		font-size: 12px;
		color: #FFD700;
	}

	.time {
		font-size: 12px;
		color: #666;
	}

	.card-body {
		margin-bottom: 20px;
	}

	.info-row {
		display: flex;
		margin-bottom: 8px;
	}

	.label {
		width: 60px;
		color: #888;
		font-size: 13px;
	}

	.value {
		color: #ccc;
		font-size: 13px;
	}

	.card-footer {
		display: flex;
		gap: 15px;
	}

	.btn {
		flex: 1;
		font-size: 14px;
		height: 36px;
		line-height: 36px;
		border-radius: 18px;
		border: none;
	}

	.btn-reject {
		background-color: #2a2a2a;
		color: #ccc;
	}

	.btn-approve {
		background: linear-gradient(45deg, #FFD700, #FFA500);
		color: #000;
		font-weight: bold;
	}
	
	.empty-state {
		text-align: center;
		padding: 40px 0;
		color: #666;
		font-size: 14px;
	}
</style>
