<template>
	<view class="container">
		<uni-card :cover="cover" @click="onClick">
			<!-- <image slot='cover' style="width: 100%;" :src="cover"></image> -->
			<!-- <text class="uni-body">这是一个带封面和操作栏的卡片示例，此示例展示了封面插槽和操作栏插槽的用法。</text> -->
			<uni-group :title="'《' + title + '》- ' + author" type="line" margin-top="20">
				<view v-for="v in this.paragraphs"> {{v}} </view>
			</uni-group>
			<view slot="actions" class="card-actions">
				<!-- <view class="card-actions-item" @click="actionsClick('分享')">
					<uni-icons type="redo" size="18" color="#999"></uni-icons>
					<text class="card-actions-item-text">分享</text>
				</view> -->
				<view class="card-actions-item" @click="actionsClick('点赞')">
					<uni-icons type="heart" size="18" color="#999"></uni-icons>
					<text class="card-actions-item-text">点赞</text>
				</view>
				<view class="card-actions-item" @click="refreshClick('评论')">
					<uni-icons type="reload" size="18" color="#999"></uni-icons>
					<text class="card-actions-item-text">刷新</text>
				</view>
			</view>
		</uni-card>
		
	</view>
</template>

<script>
	console.log(process.env.VUE_APP_SERVICE_URL)
	const requestUrl = process.env.VUE_APP_SERVICE_URL + "/yuanfang/rand_tssc";

	export default {
		data() {
			return {
				paragraphs:[],
				author:"",
				title:"",
			}
		},
		onLoad(){
			this.initData()
		},
		methods: {
			async initData() {
				uni.request({
					url: requestUrl,
					dataType: 'text',
					data: {
						noncestr: Date.now()
					},
					success: (res) => {
						let allData = JSON.parse(res.data)
						console.log(111, allData)
						this.paragraphs = JSON.parse(allData.data.paragraphs)
						this.author = allData.data.author
						this.title = allData.data.title
					},
					fail: (err) => {
						console.log('request fail', err);
						
					},
					complete: () => {
						this.loading = false;
					}
				});
			},
			refreshClick(text) {
				this.initData()
			},
			actionsClick(text) {
				uni.showToast({
					title: text,
					icon: 'none'
				})
			}
		}
	}
</script>

<style>
	.container {
		padding: 20px;
		font-size: 14px;
		/* background-color: aqua; */
	}
	.card-actions {
		display: flex;
		flex-direction: row;
		justify-content: space-around;
		align-items: center;
		height: 45px;
		border-top: 1px #eee solid;
	}
	.card-actions-item {
		display: flex;
		flex-direction: row;
		align-items: center;
	}
	.card-actions-item-text {
		font-size: 12px;
		color: #666;
		margin-left: 5px;
	}
</style>
