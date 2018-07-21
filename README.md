## from表单验证
### 一、类型验证
* type
> email、url、number、range、date(date、month、week、time、datetime、datetime-local)、search、color、tel等

### 二、代码实例
```
<!--
action：后台提交地址
method:提交方式 get、post等
enctype:multipart/form-data
enctype属性主要针对表单中有 <input type="file"> 的时候必须要加的属性，因为有formdata要上传到后台去

required:表单必填
autofocus:自动聚焦
novalidate:不让表单验证(用在form上)
formnovalidate：不让表单验证(用在type=submit的input上)

pattern:正则验证
autocomplete:自动填充  默认是on

-->
<form action=""  method="" enctype="multipart/form-data" autocomplete="off" >
    <input type="file">
    <label for="">用户名</label>
    <input type="text" name="user" placeholder="请输入用户名" required autofocus="autofocus">
    <label for="">工号</label>
    <input type="text" name="gonghso" placeholder="请输入用户名" pattern="^\d{5}[imooc]$">

    <!--
     dataList使用案例
   -->
    <input type="text" list="tips">
    <dataList id="tips">
        <option value="value">sdsd</option>
        <option value="value2">4</option>
        <option value="value4">6</option>
    </dataList>

    <!--
    label的属性用法
     这个标签可以通过for和input上的id关联起来 点击文字也可以触发单选
    -->
    <label for="man">男</label>
    <input type="radio" name="sex" id="man" required>
    <label for="woman">女</label>
    <input type="radio" name="sex" id="woman" required>

    <!--<input type="submit" formnovalidate>-->
    <input type="submit"  >
</form>

```
### 三、html约束验证API
* willValidate属性
* validity 属性
* validtionMessage属性
* checkValidity()方法
> 如果元素没有满足他的任意约束，返回false，其他情况返回true
```
 <input type="email"  value="981174580@qq.com" name="email"  id="email">
 <input type="email"  value="98117" name="email"  id="email2">
 <script>
    console.log(email.checkValidity())  //true
    console.log(email2.checkValidity())  //false
 </script>
 ```
* setCustomValidity()方法
> 设置自定义验证信息
```
    <label for="">测试</label>
    <input type="text" name="text" pattern="^\d{5}[imooc]$"  required oninput="checkit(this)">
 <script>
     function  checkit(obj){
            console.log(obj.validity)
            var it=obj.validity;
            if(it.valueMissing){
                obj.setCustomValidity('不能为空')
            } else {
               if(it.patternMismatch){
                   obj.setCustomValidity('格式错误')
               } else{
                   obj.setCustomValidity('')
               }
            }
        }
 </script>
```

```
    /*
        * willValidate属性
        * validity 属性
        * validtionMessage属性
        * checkValidity()方法
        * setCustomValidity()方法
* */

    let user=document.getElementById('user');
    console.log("validity",user.validity)
    /*
    打印结果
    * badInput:false, 用户提供了一个浏览器不能转换的input
      customError:false,//setClustomValidity()
      patternMismatch:false,//patter  验证不通过是为true
      rangeOverflow:false,//max
      rangeUnderflow:false,//min
      stepMismatch:false,//step
      tooLong:false,//maxlength
      tooShort:false,//minlength
      typeMismatch:false,//不符合某种类型，例如email、url、tel等
      valid:false,//只要所有都是false他就会变成true   如果input有默认值他也会变为true
      valueMissing:true//和requre对应    如果input里面有value值，那么他会变位false
    * */

```

###  四、表单伪类控制
> required 、optional 、in-range 、out-of-range、valid、invalid、read-only、read-write

```
<style>
      /*区分必填和选填*/
      input:required{
       border-right:3px solid red;
      }
      input:optional{
        border-right:3px solid blue;
      }

    /*去掉 type=seach的清除按钮*/
     input[type=search]::-webkit-search-cancel-button{
         -webkit-appearance: none;
         height: 15px;
         width: 15px;
         background-color: red;
     }

    /*去掉 type=number的箭头*/
    input[type=number]::-webkit-inner-spin-button,
    input[type=number]::-webkit-outer-spin-button{
        -webkit-appearance: none;
        margin: 0;
    }
</style>

```
