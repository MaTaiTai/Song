<template>
	<view class="container">
		<!-- Profile Header -->
		<view class="profile-header">
			<view class="avatar">
				<text class="avatar-text">S</text>
			</view>
			<view class="profile-info">
				<text class="singer-name">Jason (驻场)</text>
				<text class="singer-status">状态: 在线接单中</text>
			</view>
			<view class="settings-btn">
				<text class="settings-icon">⚙️</text>
			</view>
		</view>

		<!-- Income Card -->
		<view class="income-card">
			<view class="income-row">
				<view class="income-item">
					<text class="income-label">今日收益 (元)</text>
					<text class="income-value">¥320.00</text>
				</view>
				<view class="income-item">
					<text class="income-label">累计收益 (元)</text>
					<text class="income-value small">¥12,450.00</text>
				</view>
			</view>
			<button class="btn-withdraw">申请提现</button>
		</view>

		<!-- Action Grid -->
		<view class="action-grid">
			<view class="action-item" @click="uploadSong">
				<view class="action-icon add">+</view>
				<text class="action-text">上传新歌</text>
			</view>
			<view class="action-item">
				<view class="action-icon">📝</view>
				<text class="action-text">歌单管理</text>
			</view>
			<view class="action-item">
				<view class="action-icon">💬</view>
				<text class="action-text">互动留言</text>
			</view>
			<view class="action-item">
				<view class="action-icon">📊</view>
				<text class="action-text">数据分析</text>
			</view>
		</view>

		<!-- Current Playlist -->
		<view class="section-title">我的歌单 (已上架)</view>
		<view class="song-list">
			<view class="song-item" v-for="(song, index) in mySongs" :key="index">
				<view class="song-info">
					<text class="song-name">{{song.name}}</text>
					<text class="song-price">¥{{song.price}}</text>
				</view>
				<view class="song-controls">
					<switch :checked="song.active" color="#FFD700" style="transform:scale(0.7)"/>
					<text class="edit-btn">编辑</text>
				</view>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				mySongs: [
					{ name: '成都 (Cover)', price: 20, active: true },
					{ name: '南山南', price: 25, active: true },
					{ name: '平凡之路', price: 30, active: false },
					{ name: '晴天', price: 20, active: true }
				]
			}
		},
		methods: {
			uploadSong() {
				uni.showToast({
					title: '点击了上传新歌',
					icon: 'none'
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

	.profile-header {
		display: flex;
		align-items: center;
		margin-bottom: 25px;
		margin-top: 10px;
	}

	.avatar {
		width: 60px;
		height: 60px;
		border-radius: 50%;
		background-color: #333;
		display: flex;
		align-items: center;
		justify-content: center;
		margin-right: 15px;
		border: 2px solid #FFD700;
	}

	.avatar-text {
		font-size: 24px;
		font-weight: bold;
		color: #FFD700;
	}

	.profile-info {
		flex: 1;
	}

	.singer-name {
		font-size: 18px;
		font-weight: bold;
		color: #fff;
		display: block;
		margin-bottom: 5px;
	}

	.singer-status {
		font-size: 12px;
		color: #4ECDC4;
	}

	.settings-icon {
		font-size: 20px;
		color: #888;
	}

	.income-card {
		background: linear-gradient(135deg, #FFD700, #FFA500);
		border-radius: 15px;
		padding: 20px;
		margin-bottom: 25px;
		box-shadow: 0 4px 15px rgba(255, 215, 0, 0.2);
	}

	.income-row {
		display: flex;
		justify-content: space-between;
		margin-bottom: 15px;
	}

	.income-item {
		display: flex;
		flex-direction: column;
	}

	.income-label {
		font-size: 12px;
		color: rgba(0,0,0,0.6);
		margin-bottom: 5px;
		font-weight: bold;
	}

	.income-value {
		font-size: 24px;
		font-weight: bold;
		color: #000;
	}
	
	.income-value.small {
		font-size: 18px;
		margin-top: 6px;
	}

	.btn-withdraw {
		background-color: rgba(0,0,0,0.1);
		color: #000;
		font-size: 14px;
		border-radius: 20px;
		border: 1px solid rgba(0,0,0,0.1);
		font-weight: bold;
	}

	.action-grid {
		display: grid;
		grid-template-columns: repeat(4, 1fr);
		gap: 10px;
		margin-bottom: 30px;
	}

	.action-item {
		background-color: #1E1E1E;
		padding: 15px 5px;
		border-radius: 12px;
		display: flex;
		flex-direction: column;
		align-items: center;
		justify-content: center;
	}

	.action-icon {
		font-size: 20px;
		margin-bottom: 8px;
		color: #ccc;
	}
	
	.action-icon.add {
		font-size: 24px;
		font-weight: bold;
		color: #FFD700;
	}

	.action-text {
		font-size: 10px;
		color: #888;
	}

	.section-title {
		font-size: 16px;
		font-weight: bold;
		color: #fff;
		margin-bottom: 15px;
		border-left: 3px solid #FFD700;
		padding-left: 10px;
	}

	.song-list {
		display: flex;
		flex-direction: column;
		gap: 12px;
	}

	.song-item {
		background-color: #1E1E1E;
		padding: 15px;
		border-radius: 12px;
		display: flex;
		justify-content: space-between;
		align-items: center;
	}

	.song-info {
		flex: 1;
	}

	.song-name {
		font-size: 15px;
		color: #fff;
		margin-bottom: 4px;
		display: block;
	}

	.song-price {
		font-size: 12px;
		color: #FFD700;
	}

	.song-controls {
		display: flex;
		align-items: center;
		gap: 10px;
	}

	.edit-btn {
		font-size: 12px;
		color: #888;
		padding: 4px 10px;
		border: 1px solid #333;
		border-radius: 15px;
	}
</style>
