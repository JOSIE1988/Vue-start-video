<template>
	<div id="helloworld">
		<div id="hello">
		    <div class="clear">
		   		<img src="../../static/images/logo.gif"  class="img1 float_r">
		      	<el-button class="float_r">搜索</el-button> 
		  		<el-autocomplete class="float_r" id="search" prefix-icon="el-icon-search" popper-class="my-autocomplete" v-model="state3" :fetch-suggestions="querySearch" placeholder="请输入内容" @select="handleSelect" icon="edit" :on-icon-click="handleIconClick" @onfocus="changeLength">
		  		<template scope="props">
				  <span class="addr">{{ props.item.skill }}</span>
				</template>
				</el-autocomplete>	
				
				<!-- <span>访问量:{{ msg }}</span> -->
				<div class="header_nav float_r">
					<ul class="nav" >
						<li v-for="(item,key) in nav_menu" @mouseover="change_pic(key)">
							<span>{{item}}</span>
							<!-- <img src="../../static/images/thumb_over1.gif" alt="" > -->
						</li>
					</ul>
				</div>
		    
		 	</div>
		</div>
  	</div>
</template>

<script>
var caution=false
function setCookie(name,value,expires,path,domain,secure) 
{
 var curCookie=name+"="+escape(value) +
 ((expires)?";expires="+expires.toGMTString() : "") +
 ((path)?"; path=" + path : "") +
 ((domain)? "; domain=" + domain : "") +
 ((secure)?";secure" : "")
 if(!caution||(name + "=" + escape(value)).length <= 4000)
 {
 document.cookie = curCookie
 }
 else if(confirm("Cookie exceeds 4KB and will be cut!"))
 {
 document.cookie = curCookie
 }
}
function getCookie(name) 
{
 var prefix = name + "="
 var cookieStartIndex = document.cookie.indexOf(prefix)
 if (cookieStartIndex == -1)
 {
 return null
 }    
 var cookieEndIndex=document.cookie.indexOf(";",cookieStartIndex+prefix.length)
 if(cookieEndIndex == -1)
 {
 cookieEndIndex = document.cookie.length
 }
 return unescape(document.cookie.substring(cookieStartIndex+prefix.length,cookieEndIndex))
}
function deleteCookie(name, path, domain) 
{
 if(getCookie(name)) 
 {
 document.cookie = name + "=" + 
 ((path) ? "; path=" + path : "") +
 ((domain) ? "; domain=" + domain : "") +
 "; expires=Thu, 01-Jan-70 00:00:01 GMT"
 }
}
function fixDate(date) 
{
 var base=new Date(0)
 var skew=base.getTime()
 if(skew>0)
 {
 date.setTime(date.getTime()-skew)
 }    
}
var now=new Date()
fixDate(now)
now.setTime(now.getTime()+365 * 24 * 60 * 60 * 1000)
var visits = getCookie("counter")
if(!visits)
{
 visits=1;
}  
else
{
 visits=parseInt(visits)+1;
}  
setCookie("counter", visits, now)
var newVisits = visits;



export default {
  name: 'shouye',
  data () {
    return {
	    msg: visits,
	    searchFor:'',
	    restaurants: [],
	    state3: '',
	    nav_menu:['首页','设计技巧','前端入门','联系我']
    }
  },
  methods:{
  	 querySearch(queryString, cb) {
        var restaurants = this.restaurants;
        var results = queryString ? restaurants.filter(this.createFilter(queryString)) : restaurants;
        // 调用 callback 返回建议列表的数据
        cb(results);
      },
      createFilter(queryString) {
        return (restaurant) => {
          return (restaurant.value.indexOf(queryString.toLowerCase()) === 0);
        };
      },
      loadAll() {
        return [
          { "value": "vue", "skill": "vue" },
          { "value": "vue插件", "skill": "vue插件" },
          { "value": "Js技巧", "skill": "JS技巧" },
          { "value": "H5新特性", "skill": "H5新特性" },
          { "value": "html基础", "skill": "html基础" }
        ];
      },
       handleSelect(item) {
        console.log(item);
      },
      handleIconClick(ev) {
        console.log(ev);
      },
      changeLength(){
      	$("#search").animate({
      		'width':'500px'
      	},500)
      },
      change_pic(key){

      }

  },
   mounted() {
      this.restaurants = this.loadAll();
    },
  created(){
    $("#search").animate({
    	"opacity":1
    },100);
  }
}
</script>
<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1, h2 {
  font-weight: normal;
}

ul {
  list-style-type: none;
  padding: 0;
}

li {
  display: inline-block;
  margin: 0 10px;
}

a {
  color: #42b983;
}
.white_box{
  background: #fff;
  border: 1px solid #f3f3f3;
  width: 900px;
  height: 200px;
  position: relative;
  left:500px;
  z-index: 2;
}
.transparent_box{
  background: transparent;
  border: 1px solid #f3f3f3;
  width: 900px;
  height: 200px; 
  left:500px;
  position: relative;
  z-index: 2;  
}
#search{
	opacity: 0;
}
.img1{
  	width: 60px;
  	vertical-align: middle;
  	/*position: relative;*/
  	top:-10px;
  	margin-right: 10px;
}
.addr{
	padding: 2px 8px;
	border:1px solid #f2f2f2;
	border-radius: 20px;
	font-size: 12px;
	display: inline-block;
	margin: 20px 5px 5px 10px;
}
.header_nav{
	display: inline-block;
}
.float_l{
	float: left;
}
.float_r{
	float: right;
}
.clear{
	overflow: hidden;
}
.nav li{
	height: 100px;
}
.header_content{
	padding-top:30px; 
}
</style>
