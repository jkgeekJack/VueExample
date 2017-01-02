大家都知道Vue.js是中国人创造出来的，简单易用，所以必须要支持一下

##**Vue采用的*MVVM*设计模式**
也就是说model和view绑定
model改变，view的内容改变，反之亦然

##**Vue主要有以下几个关键字**
1. v-model 绑定模型
2. v-if 判断是否显示该dom
3. v-show 判断是否将该dom的display设为none
4. v-else if或者show为false时显示该dom
5. v-for 迭代
6. v-bind 绑定属性
7. v-on 绑定方法

##我们以一个可查找的信息管理系统为例子

```
<!DOCTYPE html>
<html>

    <head>
        <meta charset="UTF-8">
        <title></title>
        <link rel="stylesheet" href="styles/demo.css" />
    </head>

    <body>
        <div id="app">
            <span>key</span>
            <!-- 绑定model中search.key -->
            <!-- 内容和下面每一列的数据进行比较 -->
            <!-- 内容改变，下面的每一列都马上会进行比较 -->
            <input type="text" v-model="search.key">
                <legend>
                    Create New Person
                </legend>
                <div class="form-group">
                    <label>Name:</label>
                    <!-- 绑定model中newPerson.name -->
                    <input type="text" v-model="newPerson.name"/>
                </div>
                <div class="form-group">
                    <label>Age:</label>
                    <!-- 绑定model中newPerson.age -->
                    <input type="text" v-model="newPerson.age"/>
                </div>
                <div class="form-group">
                    <label>Sex:</label>
                    <!-- 绑定model中newPerson.sex -->
                    <select v-model="newPerson.sex">
                    <option value="Male">Male</option>
                    <option value="Female">Female</option>
                </select>
                </div>
                <div class="form-group">
                    <label></label>
                    <!-- @click是v-on:click的缩写 -->
                    <button @click="createPerson">Create</button>
                </div>
        </fieldset>
        <table>
            <thead>
                <tr>
                    <th>Name</th>
                    <th>Age</th>
                    <th>Sex</th>
                    <th>Delete</th>
                </tr>
            </thead>
            <tbody>
                <!-- 用v-for迭代，$index为每一个item的索引 -->
                <!-- v-if判断为true则显示，否则则移除，这里更适合用v-show,v-show并不会移除dom只会将display属性改为none -->
                <!-- 和搜索框内容进行比较 -->
                <tr v-for="person in people" v-if="person.name.indexOf(search.key)>=0||person.sex.indexOf(search.key)>=0||person.age==search.key">
                        <td >{{ person.name }}</td>
                        <!-- :style是v-bind:style的缩写，满足条件则值为前面的，否则为后面的，固定的字符串要用' ',变量不需要用'' -->
                        <!-- v-bind后面还可以接其他的属性例如class，id -->
                        <td :style="person.age>30 ? 'color: red' : ' ' ">{{ person.age }}</td>
                        <!-- v-else元素必须立即跟在v-if或v-show元素的后面——否则它不能被识别 -->
                        <td v-if="person.sex =='Male'">男</td>
                        <td v-else>女</td>
                        <td class="text-center"><button @click="deletePerson($index)">Delete</button></td>
                </tr>
            </tbody>
        </table>
        </div>
    </body>
    <script src="js/vue.js"></script>
    <script>
        // 初始化Vue
        //el获取绑定的标签，#app获取id为app的dom，.app的话则获取class为app的dom
        //data中为模型
        //methods为方法
        var vm = new Vue({
            el: '#app',
            data: {
                search:{
                    key:""
                },
                newPerson: {
                    name: '',
                    age: 0,
                    sex: 'Male'
                },
                people: [{
                    name: 'Jack',
                    age: 30,
                    sex: 'Male'
                }, {
                    name: 'Bill',
                    age: 26,
                    sex: 'Male'
                }, {
                    name: 'Tracy',
                    age: 22,
                    sex: 'Female'
                }, {
                    name: 'Chris',
                    age: 36,
                    sex: 'Male'
                }]
            },
            methods:{
                createPerson: function(){
                    this.people.push(this.newPerson);
                    // 添加完newPerson对象后，重置newPerson对象
                    this.newPerson = {name: '', age: 0, sex: 'Male'}
                },
                deletePerson: function(index){
                    // 删一个数组元素
                    this.people.splice(index,1);
                }
            }
        })
    </script>

</html>
```

不需要太多的解释，直接看代码就知道Vue用法是什么

##效果图

![效果](http://img.blog.csdn.net/20170102094932832?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvcXFfMzIxOTgyNzc=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)

![搜索](http://img.blog.csdn.net/20170102094953513?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvcXFfMzIxOTgyNzc=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)
