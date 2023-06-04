<template>
	<view>
		<uni-section>
			<uni-group :title="'《' + chapter + '》'" type="line" margin-top="20">
				<view v-for="v in this.paragraphs"> {{v}} </view>
			</uni-group>
		</uni-section>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				paragraphs:[],
				chapter:"",
			}
		},
		methods: {
			
		},
		onLoad: function (option) {
			this.paragraphs = JSON.parse(option.paragraphs)
			this.chapter = option.chapter
		}
	}
</script>

<style>

</style>
