## 获取返回的数据

#### 打印指定变量名
格式：${变量名}

#### 在模板中为变量赋值
格式：<#assign 变量名=变量/>例如：

* 赋值：

      <#assign a="letter a" />
      <#assign b=31241243432423 />
* 打印赋值的变量

      a=${a}
      b=${b}

* 结果 

      a=letter a
      b=31,241,243,432,423

若变量为null，会报错：user:${gfagcustomerList}
应对方法：在要打印的变量后加"!",若要设置默认值，则在后面加想要显示的默认值

        user:${customerList!"default"}
若变量为list，直接打印变量，也会报错：

	user:${customerList!}

### 对结果list遍历
	<#list customerList as customer>
	userId:${customer.userId}
	</#list>
遍历前判断空：

	<#list customerList ! as customer>

#### 使用变量之前，先判断变量是否存在
语法：:<#if 变量名 ??>

	<#if csustomerList ??>
	    <#list customerList ! as customer>
	    userId:${customer.userId}---- <br/>
	    </#list>
	</#if>

#### 获取List的size,String的length
语法：:${List的变量名?size}

	${customerList?size}
