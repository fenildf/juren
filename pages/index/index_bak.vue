<template>
	<view class="index_content" :style="{height: screenHeight}">
		<scroll-view scroll-x="true" class="scroll-view" scroll-with-animation="true" :style="{height: innerHeight}">
			<view :id="welike.id" class="welike_wrapper" v-for="(welike, index) in welikeList" :key="index" @longpress="welike_detail"
			 :data-index="index" @click="hide_welike_detail" :style="{height: innerHeight}">
				<view class="welike_item">
					<!-- 封面 -->
					<view class="welike_cover_wrapper">
						<image class="welike_cover" :src="welike.imageURL" mode="aspectFill"></image>
					</view>
					<!-- 反向圆角 -->
					<view class="welike_radius">

					</view>
					<!-- 描述 -->
					<view class="welike_content">
						<view class="welike_title">
							{{welike.title}}
						</view>
						<view class="welike_desc">
							{{welike.desc}}
						</view>
					</view>
				</view>
			</view>
		</scroll-view>

	</view>
</template>

<script>
	export default {
		data() {
			return {
				screenHeight: "0",
				innerHeight: "0",
				animationData: null,
				animation: null,
				welikeList: [{
						id: 1,
						imageURL: '../../static/images/movie1.jpg',
						title: '乡村爱情11',
						desc: '该剧主要讲述了以刘能、广坤、赵四为首的象牙山村民在新时代背景下，就“精准扶贫”“招商引资”等国家惠农政策的误解，与新到任大学生村官杜小双以及到象牙山投资的神秘富豪，发生的一系列依旧搞笑无解的故事',
					},
					{
						id: 1,
						imageURL: '../../static/images/movie2.jpg',
						title: '乡村爱情11',
						desc: '该剧主要讲述了以刘能、广坤、赵四为首的象牙山村民在新时代背景下，就“精准扶贫”“招商引资”等国家惠农政策的误解，与新到任大学生村官杜小双以及到象牙山投资的神秘富豪，发生的一系列依旧搞笑无解的故事',
					},
					{
						id: 1,
						imageURL: '../../static/images/movie3.jpg',
						title: '乡村爱情11',
						desc: '该剧主要讲述了以刘能、广坤、赵四为首的象牙山村民在新时代背景下，就“精准扶贫”“招商引资”等国家惠农政策的误解，与新到任大学生村官杜小双以及到象牙山投资的神秘富豪，发生的一系列依旧搞笑无解的故事',
					}
				]
			}
		},
		onLoad() {},
		methods: {}
	}
</script>

<style>
	@import url("index.css");
</style>
