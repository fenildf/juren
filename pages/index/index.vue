<template>
	<view class="index_content">

		<jurenItems :itemList = "welikeList"></jurenItems>

	</view>
</template>

<script>
	import jurenItems from '../../componets/jurenItems.vue'
	export default {
		data() {
			return {
				welikeList: [{
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
					}
				]
			}
		},
		onLoad() {},
		methods: {},
		computed: {

		},
		components: {
			jurenItems
		}
	}
</script>

<style>
	@import url("index.css");
</style>
