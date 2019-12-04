<template>
	<view class="content" :style="{height: screenHeight}">
		<view class="view_player_wrapper">
			<video class="player" :src="content_detail.video_src" :poster="content_detail.video_poster" controls @error="video_error_callback"></video>
		</view>

		<view class="tab-panel">
			<view class="content_title_wrapper">
				<view class="title_wrapper">
					<view class="content_title">
						{{content_detail.title}}
					</view>
					<view class="content_date">
						更新日期：{{content_detail.start_date}}
					</view>
				</view>

				<!-- 顶部选项卡 -->
				<scroll-view id="nav-bar" class="nav-bar" scroll-x scroll-with-animation :scroll-left="scrollLeft">
					<view v-for="(item,index) in tabBars" :key="item.id" class="nav-item" :class="{current: index === tabCurrentIndex}"
					 :id="'tab'+index" @click="changeTab(index)">{{item.name}}</view>
				</scroll-view>
			</view>

			<!-- 内容部分 -->
			<swiper id="swiper" class="swiper-box" :duration="300" :current="tabCurrentIndex" @change="changeTab">
				<swiper-item v-for="(tabItem, index) in tabBars" :key="tabItem.id">
					<scroll-view class="panel-scroll-box" :scroll-y="enableScroll">
						<view v-if="index == 0" class="description">
							{{tabItem.data}}
						</view>
						<view v-if="index == 1" class="actors">
							<view v-for="(dataItem,index) in tabItem.data" :key="index" class="actor_wrapper">
								<image :src="dataItem.image" class="actors_image" @click="previewImage(index)"></image>
								<view class="actors_name">
									{{dataItem.name}}
								</view>
								<view class="actors_role">
									饰：{{dataItem.role}}
								</view>
							</view>
						</view>
						<view v-if="index == 2" class="sources">
							<view v-for="(dataItem,index) in tabItem.data" :key="index" class="sources_wrapper">
								<image :src="dataItem.image" class="sources_image" mode=""></image>
								<view class="sources_name">
									{{dataItem.name}}
								</view>
							</view>
						</view>
					</scroll-view>
				</swiper-item>
			</swiper>
		</view>
		<view type="warn" class="welike" @click="doLike">
			<text class="welike_font" v-if="like_flag == 0">
				想看
			</text>
			<text class="welike_font" v-if="like_flag == 1">
				已想看
			</text>
		</view>
	</view>
</template>

<script>
	let scrollTimer = false,
		tabBar;
	export default {
		data() {
			return {
				like_list: [],
				like_flag: 0,
				screenHeight: 0,
				scrollLeft: 0, //顶部选项卡左滑距离
				enableScroll: true,
				tabCurrentIndex: 0,
				content_detail: {
					id: 1,
					title: '乡村爱情11',
					video_poster: '../../static/images/movie9.jpg',
					video_src: 'https://clips.vorwaerts-gmbh.de/big_buck_bunny.mp4',
					// video_src: 'https://dcloud-img.oss-cn-hangzhou.aliyuncs.com/guide/uniapp/%E7%AC%AC1%E8%AE%B2%EF%BC%88uni-app%E4%BA%A7%E5%93%81%E4%BB%8B%E7%BB%8D%EF%BC%89-%20DCloud%E5%AE%98%E6%96%B9%E8%A7%86%E9%A2%91%E6%95%99%E7%A8%8B@20181126.mp4',
					desc: '',
					start_date: '2019-12-3'
				},
				tabBars: [{
					id: 1,
					name: '简介',
					data: '张庆熟读古典名著，但他用现代观念剖析古代文学史的论文命题不被教授所认可。为了让教授成为自己的导师，张庆通过写小说的方式阐述自己的观点。在小说中，身世神秘的少年范闲，自小生活在小城澹州，一位老师的突然造访，他看似平静的生活开始直面重重的危机与考验。' +
						'...张庆熟读古典名著，但他用现代观念剖析古代文学史的论文命题不被教授所认可。为了让教授成为自己的导师，张庆通过写小说的方式阐述自己的观点。在小说中，身世神秘的少年范闲，自小生活在小城澹州，一位老师的突然造访，他看似平静的生活开始直面重重的危机与考验。'
				}, {
					id: 2,
					name: '演职人员',
					data: [{
						name: '张若昀',
						image: 'http://qzonestyle.gtimg.cn/qzone/app/weishi/client/testimage/1024/1.jpg',
						role: '范闲'
					}, {
						name: '张若昀',
						image: '../../static/images/movie9.jpg',
						role: '范闲'
					}, {
						name: '张若昀',
						image: '../../static/images/movie9.jpg',
						role: '范闲'
					}, {
						name: '张若昀',
						image: '../../static/images/movie9.jpg',
						role: '范闲'
					}, {
						name: '张若昀',
						image: '../../static/images/movie9.jpg',
						role: '范闲'
					}, {
						name: '张若昀',
						image: '../../static/images/movie9.jpg',
						role: '范闲'
					}, {
						name: '张若昀',
						image: '../../static/images/movie9.jpg',
						role: '范闲'
					}]
				}, {
					id: 3,
					name: '播放源',
					data: [{
						name: '优酷',
						image: '../../static/images/movie9.jpg',
					}]
				}]
			}
		},
		onLoad: function(data) {
			//接收参数，发送请求
			console.log(data);

			uni.setNavigationBarTitle({
				title: this.content_detail.title
			});

			//根据屏幕高度设置内容高度
			this.screenHeight = uni.getSystemInfoSync().windowHeight + 'px';

			//判断想看按钮状态
			this.like_list = uni.getStorageSync('like_list');

			if (this.like_list.includes(this.content_detail.id)) {
				this.like_flag = 1;
			}

			//显示分享按钮
			uni.showShareMenu();
		},
		onShareAppMessage(res) {
			return {
				title: '剧人好剧推荐-' + this.content_detail.title,
				path: '/pages/content_detail/content_detail?id=1',
				imageUrl: '../../static/images/movie9.jpg'
			}
		},
		methods: {
			//tab切换
			async changeTab(e) {
				if (scrollTimer) {
					//多次切换只执行最后一次
					clearTimeout(scrollTimer);
					scrollTimer = false;
				}
				let index = e;
				//e=number为点击切换，e=object为swiper滑动切换
				if (typeof e === 'object') {
					index = e.detail.current
				}
				if (typeof e === 'number') {
					//点击切换时先切换再滚动tabbar，避免同时切换视觉错位
					this.tabCurrentIndex = index;
				}
				//延迟300ms,等待swiper动画结束再修改tabbar
				scrollTimer = setTimeout(() => {
					if (typeof e === 'object') {
						this.tabCurrentIndex = index;
					}
					this.tabCurrentIndex = index;


					//第一次切换tab，动画结束后需要加载数据
					let tabItem = this.tabBars[this.tabCurrentIndex];
					if (this.tabCurrentIndex !== 0 && tabItem.loaded !== true) {
						tabItem.loaded = true;
					}
				}, 300)

			},
			doLike: function() {
				if (this.like_flag == 1) {
					return;
				} else if (!this.like_list.includes(this.content_detail.id)) {
					this.like_list.push(this.content_detail.id);
					this.like_flag = 1;
					uni.setStorage({
						key: 'like_list',
						data: this.like_list
					})
				}
			},
			video_error_callback: function(e) {
				uni.showModal({
					content: e.target.errMsg,
					showCancel: false
				})
			},
			previewImage: function(index) {

				let imageArray = [];

				for (let var2 of this.tabBars[1].data) {
					imageArray.push(var2.image);
				}

				uni.previewImage({
					current: index,
					urls: imageArray,
					longPressActions: {
						itemList: ['发送给朋友', '保存图片'],
						success: function(data) {
							console.log('选中了第' + (data.tapIndex + 1) + '个按钮,第' + (data.index + 1) + '张图片');
						},
						fail: function(err) {
							console.log(err.errMsg);
						}
					}
				});
			}
		}
	}
</script>

<style>
	@import url("content_detail.css");
</style>
