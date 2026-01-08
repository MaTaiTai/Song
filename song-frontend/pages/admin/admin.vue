<template>
	<view class="container">
		<view class="header">
			<text class="title">管理后台</text>
			<text class="subtitle">Administrator Dashboard</text>
		</view>

		<!-- Stats Cards -->
		<view class="stats-container">
			<view class="stat-card primary">
				<text class="stat-label">今日营收</text>
				<text class="stat-value">¥1,280.00</text>
			</view>
			<view class="stat-card secondary">
				<text class="stat-label">待处理订单</text>
				<text class="stat-value">12</text>
			</view>
		</view>

		<!-- Menu Grid -->
		<view class="menu-grid">
			<view class="menu-item" v-for="(item, index) in menuItems" :key="index" @click="handleMenuClick(item)">
				<view class="icon-box" :style="{backgroundColor: item.color}">
					<text class="menu-icon">{{item.icon}}</text>
				</view>
				<text class="menu-text">{{item.text}}</text>
			</view>
		</view>
		
		<!-- Recent Orders List -->
		<view class="section-title">最近订单</view>
		<view class="order-list">
			<view class="order-item" v-for="(order, index) in recentOrders" :key="index">
				<view class="order-info">
					<text class="order-song">{{order.song}}</text>
					<text class="order-user">{{order.user}}</text>
				</view>
				<text class="order-status" :class="order.status">{{order.statusText}}</text>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				menuItems: [
					{ text: '歌手审核', icon: 'A', color: '#FF6B6B', path: '/pages/admin/audit' },
					{ text: '用户管理', icon: 'U', color: '#4ECDC4' },
					{ text: '歌单管理', icon: 'M', color: '#FFE66D' },
					{ text: '财务报表', icon: 'F', color: '#1A535C' },
					{ text: '系统设置', icon: 'C', color: '#F7FFF7' },
					{ text: '消息通知', icon: 'N', color: '#FF9F1C' }
				],
				recentOrders: [
					{ song: '告白气球', user: '张三', status: 'pending', statusText: '待播放' },
					{ song: '成都', user: '李四', status: 'playing', statusText: '播放中' },
					{ song: '海阔天空', user: '王五', status: 'completed', statusText: '已完成' }
				]
			}
		},
		onShow() {
			// Security check: Verify admin session
			const role = uni.getStorageSync('userRole');
			if (role !== 'admin') {
				uni.showToast({
					title: '登录已失效，请重新登录',
					icon: 'none',
					duration: 2000
				});
				setTimeout(() => {
					uni.reLaunch({
						url: '/pages/login/login'
					});
				}, 1500);
			}
		},
		onUnload() {
			// Clear admin session on page exit (optional, depends on requirement)
			// If we want strictly "login once per entry", we can clear here.
			// But usually "Logout" button is better. 
			// Based on user request "return and enter again should fail", we clear it.
			uni.removeStorageSync('userRole');
			uni.removeStorageSync('isLoggedIn');
		},
		methods: {
			handleMenuClick(item) {
				if (item.path) {
					uni.navigateTo({
						url: item.path
					});
				} else {
					uni.showToast({
						title: '功能开发中',
						icon: 'none'
					});
				}
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

	.stats-container {
		display: flex;
		gap: 15px;
		margin-bottom: 30px;
	}

	.stat-card {
		flex: 1;
		padding: 20px;
		border-radius: 15px;
		display: flex;
		flex-direction: column;
	}

	.stat-card.primary {
		background: linear-gradient(135deg, #FFD700, #FFA500);
	}

	.stat-card.secondary {
		background-color: #1E1E1E;
		border: 1px solid #333;
	}

	.stat-label {
		font-size: 12px;
		margin-bottom: 5px;
		color: rgba(255,255,255,0.7);
	}
	
	.secondary .stat-label {
		color: #888;
	}

	.stat-value {
		font-size: 24px;
		font-weight: bold;
		color: #fff;
	}

	.menu-grid {
		display: grid;
		grid-template-columns: repeat(3, 1fr);
		gap: 15px;
		margin-bottom: 30px;
	}

	.menu-item {
		background-color: #1E1E1E;
		padding: 20px 10px;
		border-radius: 15px;
		display: flex;
		flex-direction: column;
		align-items: center;
		justify-content: center;
	}

	.icon-box {
		width: 40px;
		height: 40px;
		border-radius: 10px;
		display: flex;
		align-items: center;
		justify-content: center;
		margin-bottom: 10px;
	}

	.menu-icon {
		font-weight: bold;
		color: #121212;
	}

	.menu-text {
		font-size: 12px;
		color: #ccc;
	}
	
	.section-title {
		font-size: 18px;
		color: #fff;
		margin-bottom: 15px;
		font-weight: bold;
	}
	
	.order-list {
		display: flex;
		flex-direction: column;
		gap: 10px;
	}
	
	.order-item {
		background-color: #1E1E1E;
		padding: 15px;
		border-radius: 10px;
		display: flex;
		justify-content: space-between;
		align-items: center;
	}
	
	.order-info {
		display: flex;
		flex-direction: column;
	}
	
	.order-song {
		color: #fff;
		font-size: 16px;
		margin-bottom: 4px;
	}
	
	.order-user {
		color: #666;
		font-size: 12px;
	}
	
	.order-status {
		font-size: 12px;
		padding: 4px 8px;
		border-radius: 4px;
	}
	
	.order-status.pending {
		background-color: rgba(255, 215, 0, 0.1);
		color: #FFD700;
	}
	
	.order-status.playing {
		background-color: rgba(78, 205, 196, 0.1);
		color: #4ECDC4;
	}
	
	.order-status.completed {
		background-color: rgba(255, 255, 255, 0.1);
		color: #888;
	}
</style>