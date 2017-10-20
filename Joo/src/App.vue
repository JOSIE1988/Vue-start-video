<template>
	<div id="app">
		<router-view/>
		<!-- <img src="../static/images/cherry_bac.png" alt="" class="bac"> -->
	</div>
</template>

<script>
export default {
  	name: 'app',
  	data(){
  		return{
  		
  		}
  		
  	},
  	beforecreate(){

  	},
  	created() {
      try {
        document.body.removeChild(document.getElementById('appLoading'))
        setTimeout(function() {
          document.getElementById('app').style.display = 'block';
        }, 500)
      } 
      catch (e) {

      }
    }
}
</script>

<style>
#app {
  font-family: "Helvetica Neue",Helvetica,"PingFang SC","Hiragino Sans GB","Microsoft YaHei","微软雅黑",Arial,sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
}
.bac{
  position: fixed;
  top:450px;
  left: 20px;
}
</style>
