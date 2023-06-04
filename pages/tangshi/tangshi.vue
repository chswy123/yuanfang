<template>
	<view>
		<uni-section title="" type="line">
			<uni-list v-for="listV in list">
				<uni-list-item ellipsis="1" :title="'《' + listV.title + '》'" :note="'唐-' + listV.author" @click="onClick($event, listV.paragraphs, listV.title)" to="`./tangshi_txt`" showArrow/>
				<!-- <uni-list-item ellipsis="1" title="《春晓》" note="唐 孟浩然" showArrow/> -->
			</uni-list>
		</uni-section>
	</view>
</template>

<script>
	console.log(process.env.VUE_APP_SERVICE_URL)
	const requestUrl = process.env.VUE_APP_SERVICE_URL + "/yuanfang/tssbs"; // todo
	
	export default {
		data() {
			return {
				list:[],
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
						this.list = allData.data
						
					},
					fail: (err) => {
						console.log('request fail', err);
						
					},
					complete: () => {
						this.loading = false;
					}
				});
			},
			onClick(e, paragraphs, title) {
				uni.navigateTo({
					url: './tangshi_txt?paragraphs=' + paragraphs + "&title=" + title
				})
			},
			// navigateTo(paragraphs, title) {
			// 	uni.navigateTo({
			// 		url: './tangshi_txt?paragraphs=' + paragraphs + "&title=" + title
			// 	})
			// },
		}
	}
</script>

<style>

</style>
