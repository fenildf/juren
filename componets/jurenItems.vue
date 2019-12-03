<template>
	<view class="list_wrapper">
		<view :id="tvItem.id" class="welike_wrapper" v-for="(tvItem, index) in itemList" :key="index" :data-index="index">
			<view class="welike_item">
				<!-- 封面 -->
				<view class="welike_cover_wrapper">
					<image class="welike_cover" :src="tvItem.imageURL" mode="aspectFill"></image>
				</view>
				<view class="welike_desc">
					<view class="welike_desc_title">{{tvItem.title}}</view>
					<image src="../static/images/end.png" v-if="tvItem.end_flag" class="end_tag"></image>
				</view>
			</view>
		</view>
	</view>
</template>

<script>
	export default {

		name: "jurenItems",

		data() {
			return {};
		},

		props: {

			itemList: {
				type: Array
			}
		},
		created() {
			// console.log(this.itemList);
		}

	}
</script>

<style>
	.list_wrapper {
		/* width: 100%; */
		padding-left: 20upx;
		padding-right: 20upx;
		padding-top: 20upx;
		display: flex;
		flex-direction: row;
		flex-wrap: wrap;
		justify-content: space-between;
	}

	.welike_wrapper {
		width: 230upx;
		height: 400upx;
	}


	.welike_item {
		width: 100%;
		height: 100%;
		/* margin-top: 120%; */
		position: relative;
	}

	.welike_cover {
		width: 100%;
		height: 100%;
		border-radius: 10rpx;
		box-shadow: 5upx 5upx 5upx #C0C0C0;
	}

	.welike_cover_wrapper {
		width: 100%;
		height: 85%;
		border-radius: 5upx 5upx 0upx 0upx;
	}

	.welike_desc {
		color: #808080;
		text-align: center;
	}

	.welike_desc_title {
		width: 80%;
		display: inline-block;
		white-space: nowrap;
		overflow: hidden;
		text-overflow: ellipsis;
	}

	.end_tag {
		width: 35upx;
		height: 35upx;
	}
</style>
