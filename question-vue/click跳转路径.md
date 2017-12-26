## click跳转路径
##### 当前文件路径是 localhost:8000/vipcard
> 例：点击事件跳转路径

```
<templete>
    <div class="" @click="bugCart">购买<div>
</templete>

<script>
    export default {
        methods: {
            buyCart(){
                this.$router.push('/confirmOrder/payment');
            }
        }
    }	
```
点击之后路径为 localhost:8000/confirmOrder/payment
> 例：点击事件跳转路径(传参跳转)

```
<templete>
    <div class="" @click="bugCart('/confirmOrder/payment')">购买<div>
</templete>

<script>
    export default {
    	methods: {
    	    buyCart(path){
                this.$router.push(path);
            }
    	}
    }	
</script>
```
点击之后路径为带参数 localhost:8000/confirmOrder/payment
> 例：点击事件跳转路径(跳转路径后代参数)

```
<templete>
    <div class="" @click="bugCart">购买<div>
</templete>

<script>
    export default {
    	methods: {
    	    buyCart(){
                this.$router.push({path:'/confirmOrder/payment', query:{num: 1}});
            }
    	}
    }	
</script>
```
点击之后路径为带参数 localhost:8000/confirmOrder/payment?num=1
> 例：点击事件跳转路径(只做路由替换，不计算步长)

```
<templete>
    <div class="" @click="bugCart">购买<div>
</templete>

<script>
    export default {
    	methods: {
    	    buyCart(){
                this.$router.replace({path:'/confirmOrder/payment', query:{num: 1}});
            }
        }
    }	
</script>
```