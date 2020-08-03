<template>
	<view>
		<button @click="get">发送get请求</button>
		<button type="primary" @click="setStroage">存储数据</button>
		<button type="primary" @click="getStroage">获取数据</button>
		<button type="primary" @click="removeId">移除id</button>
		<view>这是列表页</view>
		<view v-for="item in list" class="box">{{item}}</view>
		<!-- <button @click="pullDown">按钮</button> -->
	</view>
</template>

<script>
	export default {
		data() {
			return {
				list: ['前端', 'UI', 'Java', '大数据', 'UI', '前端', 'Java', '大数据']
			}
		},
		onPullDownRefresh() {
			console.log('下拉刷新了');
			setTimeout(() => {
				this.list = ['UI', '前端', 'Java', '大数据']
				uni.stopPullDownRefresh();
			}, 2000)
		},
		onReachBottom(){
			console.log('滚动到底了')
			this.list = [...this.list,...'Java', 'UI', '前端', '大数据']
		},
		methods: {
			pullDown(){
				uni.startPullDownRefresh();
			},
			get(){
				uni.request({
					url: 'https://pic.downk.cc/item/5d2b30cd451253d1784184f0.jpg',
					success: (res) => {
						console.log(res)
					}
				})
			},
			setStroage(){
				// uni.setStorage({
				//     key: 'id',
				//     data: 80,
				//     success: function () {
				//         console.log('存储数据');
				//     }
				// });
				uni.setStorageSync('id', 100);
			},
			getStroage(){
				// uni.getStorage({
				//     key: 'id',
				//     data: 80,
				//     success: function (res) {
				//         console.log('获取数据', res.data);
				//     }
				// });
				const value = uni.getStorageSync('id');
				console.log(value)
			},
			removeId(){
				// uni.removeStorage({
				// 	key: 'id',
				// 	success: function(){
				// 		console.log('移除成功')
				// 	}
				// })
				 uni.removeStorageSync('id');
			}
		}
	}
</script>

<style>
	.box {
		height: 100px;
		line-height: 100px;
	}
</style>
