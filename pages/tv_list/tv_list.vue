<template>
	<view class="content">

		<view class="search_panel">

			<view class="search_box">
				<icon :type="icon_type" size="15" class="search_icon" />
				<input type="text" class="search" size="50" :placeholder="search_hot_word">

				</input>
			</view>
			<view class="search_type">
				<view class="search_type_item">
					<view :class="languages_item_classes[0]" :data-class-array="languages_item_classes" :data-index="0"
					 data-class-name="languages_item_classes" @click="item_click">
						所有语种
					</view>
					<view class="item_list" v-for="(litem, index) in languages_items" @key="index" :data-class-array="languages_item_classes"
					 :data-index="index + 1" data-class-name="languages_item_classes" @click="item_click">
						<text :class="languages_item_classes[index + 1]">{{litem}}</text>
					</view>
				</view>

				<view class="search_type_item">
					<view :class="source_item_classes[0]" :data-class-array="source_item_classes" :data-index="0" data-class-name="source_item_classes"
					 @click="item_click">
						所有播放源
					</view>
					<view class="item_list" v-for="(litem, index) in source_items" @key="index" :data-class-array="source_item_classes"
					 :data-index="index + 1" data-class-name="source_item_classes" @click="item_click">
						<text :class="source_item_classes[index + 1]">{{litem}}</text>
					</view>
				</view>

				<view class="search_type_item">
					<view :class="update_item_classes[0]" :data-class-array="update_item_classes" :data-index="0" data-class-name="update_item_classes"
					 @click="item_click">
						所有更新状态
					</view>
					<view class="item_list" v-for="(litem, index) in update_items" @key="index" :data-class-array="update_item_classes"
					 :data-index="index + 1" data-class-name="update_item_classes" @click="item_click">
						<text :class="update_item_classes[index + 1]">{{litem}}</text>
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
				languages_items: ['国产剧', '美剧', '韩剧', '日剧', '其他'],
				source_items: ['优酷', '爱奇艺', '搜狐', '腾讯', '其他'],
				update_items: ['完结', '更新中', '即将播放'],
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
				for (var i = 0; i < classArray.length; i++) {

					if (classArray[i].length > 1) {
						classArray[i].pop();
					}
				}
				classArray[e.currentTarget.dataset.index].push('search_item_active');
				this[e.currentTarget.dataset.className] = classArray;
				//发送请求
				
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
