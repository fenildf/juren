<script>
	export default {
		onLaunch: function() {
			console.log('App Launch')
			//判断想看按钮状态
			let like_list = uni.getStorage({
				key: 'like_list'
			});
			
			if (like_list == null) {
				uni.setStorage({
					key: 'like_list',
					data: []
				})
			}
		},
		onShow: function() {
			console.log('App Show')
		},
		onHide: function() {
			console.log('App Hide')
		}
	}
</script>

<style>
	/*每个页面公共css */
	.content {
		display: flex;
		flex-direction: column;
		align-items: center;
		justify-content: center;
	}
</style>
