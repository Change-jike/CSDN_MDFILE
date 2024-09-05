> 本文由 [简悦 SimpRead](http://ksria.com/simpread/) 转码， 原文地址 [blog.csdn.net](https://blog.csdn.net/qq_43371422/article/details/127880308?spm=1001.2014.3001.5502)

#### input 标签 hidden 属性参数的来源与作用：

跳转接口拼装参数与前端 **<input type=“hidden” …/>** 标签属于赋值关系；

后台对应接口完成参数拼装，将参数放在 view 视图中返回前端页面，前端通过 **th:value = "${dictJson}** 接受指定参数；

参数不会展示在页面上但是会保持持有状态，随用随取；

```
ModelAndView view = new ModelAndView();
view.addObject("dictJson", dictJson);
    
-------------------------------------------------------------
// input 标签
<input type="hidden" id="dictJson" th:value="${dictJson}"/>

```

#### 主页面与子页面的数据冲突问题：

相似的页面跳转或弹框时，常带用相似的参数（变量名、数据类型相似），但是在使用时如过调用错误会导致数据混乱；

```
/*
	* 调起详情一版化页面 展示信息混乱
	* collectId-calls 点击事件页面部分（即触发一版化详情页面的主页面部分）的 collectId 
	* 可能与一版化详情页面的 collectId 冲突；
	* 因为主页面的 collectId 优先级更高，一版化页面 查询详情信息时就可能使用错误的 collectId，
    * 从而导致一版化详情信息展示混乱；
	* 可以选择修改 主页面的 collectId 命名，或者 修改一版化页面的 collectId 命名,
	* 但是一般情况下，主页面的复用率比较高，所以尽量选择修改 一版化页面的 collectId，保证影响最少的代码；
*/
// 将子页面的 id 重命名成其他
<input type="hidden" id="collectId-calls" ${collectId}"/>
-------------------------------------
<script type="text/javascript">
    /*<![CDATA[*/

	$('#addresListtables').on('click', 'tr', function () {
        var collectId = $("#collectId-calls").val();
    sessionStorage.setItem('firstCollectId',collectId);
	// 再调用时就是自己页面的 collectId 了
    utils.getNewDetail("/gang/relation-analysis", moblies, moblies, collectId, null, 1, null, null, null, null, null, "1");
    })

    /*]]>*/
</script>



```