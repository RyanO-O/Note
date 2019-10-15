实现跑马灯效果的分析：

1. 给按钮绑定 点击事件 用v-on 或者@
2. 在按钮的事件处理函数中 写相关业务逻辑代码：
    + 拿到msg字符串，调用substring进行字符串的截取操作（截取第一个放到最后位置）
3. 为了实现“跑起来”的效果，也就是自动循环截取功能，需把步骤2放到定时器

步骤：
1. 导入vue包
2. 创建控制区域
3. 定义vue实例

注意：
1. 在vue实例中，需通过this.属性/方法名，才能访问data的数据和methods的方法
2. vm实例会监听data中的数据变化并同步到html
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
    <!-- 1.导入vue包 -->
    <script src="../js/vue.js"></script>
</head>
<body>
    <!-- 2.创建控制区域 -->
    <div id="app">
        <input type="button" value="run!" v-on:click="run">
        <input type="button" value="stop!">
        <h4>{{msg}}</h4>
    </div>
    <!-- 3.定义vue实例 -->
    <script>
    // 注意：在vue实例中，需通过this.属性/方法名，才能访问data的数据和methods的方法
    var vm = new Vue({
        el:'#app',
        data:{
            msg:'走过路过千万不要错过，清仓大减价 ! ! !'
        },
        methods: {
            run(){
                // var _this = this
                setInterval(() =>{
                    // 获取开头第一个字符
                    var head = this.msg.substring(0,1)
                    // 获取第一个之后的所有字符
                    var tail = this.msg.substring(1)
                    // 重新拼接得到的字符串并赋值给this.msg
                    this.msg = tail + head
                    // 注意：vm实例会监听data中的数据变化并同步到html
                },400)
            }
        }
    })
    </script>
</body>
</html>
```