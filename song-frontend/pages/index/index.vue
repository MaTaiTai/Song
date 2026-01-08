<template>
	<view class="container">
		<!-- Header -->
		<view class="header">
			<view class="title">
				<text class="title-main">同仁四季</text>
				<text class="title-sub">Music & Coconut Chicken</text>
			</view>
			<view class="search-bar">
				<text class="search-placeholder">搜索歌手或歌曲...</text>
			</view>
		</view>

		<!-- Featured Singer -->
		<view class="section-title">今日驻唱</view>
		<scroll-view class="singer-scroll" scroll-x="true">
			<view class="singer-card" v-for="(singer, index) in singers" :key="index">
				<view class="singer-avatar" :style="{backgroundColor: singer.color}">
					<text class="singer-initial">{{singer.name[0]}}</text>
				</view>
				<text class="singer-name">{{singer.name}}</text>
				<text class="singer-style">{{singer.style}}</text>
			</view>
		</scroll-view>

		<!-- Song List -->
		<view class="section-title">热门歌单</view>
		<view class="song-list">
			<view class="song-item" v-for="(song, index) in songs" :key="index">
				<view class="song-info">
					<text class="song-name">{{song.name}}</text>
					<text class="song-artist">{{song.artist}}</text>
				</view>
				<view class="song-action">
					<text class="song-price">¥{{song.price}}</text>
					<button class="btn-order">点歌</button>
				</view>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				singers: [
					{ name: 'Jason', style: '民谣/吉他', color: '#FF6B6B' },
					{ name: 'Alice', style: '流行/钢琴', color: '#4ECDC4' },
					{ name: 'Rock', style: '摇滚/乐队', color: '#FFE66D' }
				],
				songs: [
					{ name: '成都', artist: '赵雷', price: 20 },
					{ name: '告白气球', artist: '周杰伦', price: 30 },
					{ name: '消愁', artist: '毛不易', price: 25 },
					{ name: '海阔天空', artist: 'Beyond', price: 50 },
					{ name: 'Mojito', artist: '周杰伦', price: 30 }
				]
			}
		},
		methods: {

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
		margin-bottom: 30px;
	}

	.title-main {
		font-size: 28px;
		font-weight: bold;
		color: #FFD700;
		display: block;
	}

	.title-sub {
		font-size: 14px;
		color: #888;
		letter-spacing: 2px;
	}

	.search-bar {
		margin-top: 15px;
		background-color: #2C2C2C;
		padding: 10px 15px;
		border-radius: 20px;
	}

	.search-placeholder {
		color: #666;
		font-size: 14px;
	}

	.section-title {
		font-size: 18px;
		font-weight: bold;
		color: #fff;
		margin-bottom: 15px;
		border-left: 4px solid #FFD700;
		padding-left: 10px;
	}

	.singer-scroll {
		white-space: nowrap;
		margin-bottom: 30px;
	}

	.singer-card {
		display: inline-block;
		width: 100px;
		margin-right: 15px;
		text-align: center;
		background-color: #1E1E1E;
		padding: 15px;
		border-radius: 12px;
	}

	.singer-avatar {
		width: 60px;
		height: 60px;
		border-radius: 50%;
		margin: 0 auto 10px;
		display: flex;
		align-items: center;
		justify-content: center;
	}

	.singer-initial {
		font-size: 24px;
		font-weight: bold;
		color: #fff;
	}

	.singer-name {
		display: block;
		font-size: 14px;
		color: #fff;
		margin-bottom: 4px;
	}

	.singer-style {
		font-size: 12px;
		color: #888;
	}

	.song-list {
		display: flex;
		flex-direction: column;
		gap: 15px;
	}

	.song-item {
		display: flex;
		justify-content: space-between;
		align-items: center;
		background-color: #1E1E1E;
		padding: 15px;
		border-radius: 12px;
		box-shadow: 0 4px 6px rgba(0,0,0,0.1);
	}

	.song-info {
		flex: 1;
	}

	.song-name {
		display: block;
		font-size: 16px;
		color: #fff;
		margin-bottom: 4px;
	}

	.song-artist {
		font-size: 12px;
		color: #888;
	}

	.song-action {
		display: flex;
		align-items: center;
		gap: 10px;
	}

	.song-price {
		color: #FFD700;
		font-weight: bold;
	}

	.btn-order {
		background: linear-gradient(45deg, #FFD700, #FFA500);
		color: #000;
		font-size: 12px;
		border-radius: 20px;
		padding: 0 15px;
		line-height: 28px;
		font-weight: bold;
		border: none;
	}
</style>
