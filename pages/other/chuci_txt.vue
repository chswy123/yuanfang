<template>
	<view>
		<uni-section>
			<uni-group :title="'《' + title + '》'" type="line" margin-top="20">
				<view v-for="v in this.content"> {{v}} </view>
			</uni-group>
		</uni-section>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				content:[],
				title:"",
			}
		},
		methods: {
			
		},
		onLoad: function (option) {
			this.content = JSON.parse(option.content)
			this.title = option.title
		}
	}
</script>

<style>

</style>
