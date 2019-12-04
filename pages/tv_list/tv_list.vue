<template>
	<view class="content">

		<view class="search_panel">

			<view class="search_box">
				<icon :type="icon_type" size="15" class="search_icon" />
				<input type="text" class="search" :placeholder="search_hot_word" @input="inputChange">

				</input>
			</view>
			<view class="search_type">
				<view class="search_type_item">
					<view :class="languages_item_classes[0]" :data-class-array="languages_item_classes" :data-index="0"
					 data-class-name="languages_item_classes" @click="item_click">
						所有语种
					</view>
					<view class="item_list" v-for="(litem, index) in languages_items" :key="index" :data-class-array="languages_item_classes"
					 :data-index="index + 1" data-class-name="languages_item_classes" @click="item_click">
						<text :class="languages_item_classes[index + 1]">{{litem.text}}</text>
					</view>
				</view>

				<view class="search_type_item">
					<view :class="source_item_classes[0]" :data-class-array="source_item_classes" :data-index="0" data-class-name="source_item_classes"
					 @click="item_click">
						所有播放源
					</view>
					<view class="item_list" v-for="(litem, index) in source_items" :key="index" :data-class-array="source_item_classes"
					 :data-index="index + 1" data-class-name="source_item_classes" @click="item_click">
						<text :class="source_item_classes[index + 1]">{{litem.text}}</text>
					</view>
				</view>

				<view class="search_type_item">
					<view :class="update_item_classes[0]" :data-class-array="update_item_classes" :data-index="0" data-class-name="update_item_classes"
					 @click="item_click">
						所有更新状态
					</view>
					<view class="item_list" v-for="(litem, index) in update_items" :key="index" :data-class-array="update_item_classes"
					 :data-index="index + 1" data-class-name="update_item_classes" @click="item_click">
						<text :class="update_item_classes[index + 1]">{{litem.text}}</text>
					</view>
				</view>
			</view>
		</view>
		<view class="search_white_space">

		</view>
		<view class="tv_list">
			<jurenItems :itemList="search_list"></jurenItems>
		</view>

		<!-- 上拉加载 -->
		<uni-load-more :status="loadingType"></uni-load-more>
	</view>
</template>

<script>
	import jurenItems from '../../componets/jurenItems.vue';
	import uniLoadMore from '../../componets/uni/uni-load-more.vue';

	export default {
		data() {
			return {
				icon_type: 'search',
				search_hot_word: '庆余年',
				loadingType: 'nomore',
				search_param: {
					searchWord: this.search_hot_word,
					lanaguage: null,
					source: null,
					updateStatus: null
				},
				languages_item_classes: [
					['search_type_item_title', 'search_item_active'],
					['item'],
					['item'],
					['item'],
					['item'],
					['item']
				],
				source_item_classes: [
					['search_type_item_title', 'search_item_active'],
					['item'],
					['item'],
					['item'],
					['item'],
					['item']
				],
				update_item_classes: [
					['search_type_item_title', 'search_item_active'],
					['item'],
					['item'],
					['item']
				],
				languages_items: [{
					text: '国产剧',
					value: 1
				}, {
					text: '美剧',
					value: 2
				}, {
					text: '韩剧',
					value: 3
				}, {
					text: '日剧',
					value: 4
				}, {
					text: '其他',
					value: 5
				}],
				source_items: [{
					text: '优酷',
					value: 1
				}, {
					text: '爱奇艺',
					value: 2
				}, {
					text: '搜狐',
					value: 3
				}, {
					text: '腾讯',
					value: 4
				}, {
					text: '其他',
					value: 5
				}],
				update_items: [{
					text: '完结',
					value: 1
				}, {
					text: '更新中',
					value: 2
				}, {
					text: '即将播放',
					value: 3
				}],
				search_list: [{
						id: 1,
						imageURL: '../static/images/movie1.jpg',
						title: '乡村爱情11啊实打实大苏打',
						end_flag: false
					},
					{
						id: 2,
						imageURL: '../static/images/movie3.jpg',
						title: '乡村爱情11',
						end_flag: true
					},
					{
						id: 3,
						imageURL: '../static/images/movie3.jpg',
						title: '乡村爱情11',
						end_flag: false
					},
					{
						id: 4,
						imageURL: '../static/images/movie4.jpg',
						title: '乡村爱情11',
						end_flag: false
					},
					{
						id: 5,
						imageURL: '../static/images/movie5.jpg',
						title: '乡村爱情11',
						end_flag: false
					},
					{
						id: 6,
						imageURL: '../static/images/movie6.jpg',
						title: '乡村爱情11',
						end_flag: false
					},
					{
						id: 7,
						imageURL: '../static/images/movie7.jpg',
						title: '乡村爱情11',
						end_flag: false
					},
					{
						id: 8,
						imageURL: '../static/images/movie8.jpg',
						title: '乡村爱情11',
						end_flag: false
					},
					{
						id: 9,
						imageURL: '../static/images/movie8.jpg',
						title: '乡村爱情11',
						end_flag: false
					},
					{
						id: 7,
						imageURL: '../static/images/movie7.jpg',
						title: '乡村爱情11',
						end_flag: false
					},
					{
						id: 8,
						imageURL: '../static/images/movie8.jpg',
						title: '乡村爱情11',
						end_flag: false
					},
					{
						id: 9,
						imageURL: '../static/images/movie8.jpg',
						title: '乡村爱情11',
						end_flag: false
					}
				]
			}
		},
		methods: {
			item_click: function(e) {
				// 样式变化
				let classArray = e.currentTarget.dataset.classArray;
				let index = e.currentTarget.dataset.index;
				for (var i = 0; i < classArray.length; i++) {

					if (classArray[i].length > 1) {
						classArray[i].pop();
					}
				}
				classArray[index].push('search_item_active');
				this[e.currentTarget.dataset.className] = classArray;
				
				//每次点击更新参数
				if (e.currentTarget.dataset.className.includes('language')) {
					this.search_param.lanaguage = this.languages_items[index - 1].value;
				} else if (e.currentTarget.dataset.className.includes('source')) {
					this.search_param.source = this.source_items[index - 1].value;
				} else if (e.currentTarget.dataset.className.includes('update')) {
					this.search_param.updateStatus = this.update_items[index - 1].value;
				}
				
				//发送请求
				// console.log(this.search_param);
				this.searchRequest();

			},
			inputChange: function(e) {
				this.search_param.searchWord = e.detail.value;
				this.searchRequest();
			},
			searchRequest: function() {
				console.log('发送请求！');
				
				uni.showLoading({
					title: '加载中'
				});
				
				setTimeout(function(){
					uni.hideLoading();
				}, 500);
				
				
				// uni.request({
				// 	url:'',
				// 	method: 'POST',
				// 	data: this.search_param,
				// 	success: (res) => {
				// 		console.log(res);
				// 	}
				// })
			}
		},
		onReachBottom: function() {
			// console.log('加载更多！');
		},
		components: {
			jurenItems,
			uniLoadMore
		}
	}
</script>

<style>
	@import url("tv_list.css");
</style>
