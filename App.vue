<script>
	export default {
		onLaunch: function() {
			console.log('App Launch')
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
	.dis{
		display: flex;
	}
	.cl{
		flex-direction: column;
	}
	.al_c{
		align-items: center;
	}	
	.j_c{
		justify-content: center;
	}
	.aro{
		justify-content: space-around;
	}
</style>
