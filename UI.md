## UI框架 UI Frameworks

Bootstrap
Ionic
Foundation
FrozenUI
materializecss
mui
Ant Design
eleme

# react
[markerikson/react-redux-links: Curated tutorial and resource links I've collected on React, Redux, ES6, and more](https://github.com/markerikson/react-redux-links)
[React For Beginners — The best way to learn React](https://reactforbeginners.com/)

## UI组件


ui流程
模型
ajax封装【header，mask，错误处理】

以数据为核心
ajaxdata->html
- map
    枚举，日期，null
-
- text val 控件特殊方法



html
布局

## UI
1. id
2. state
3. model

# 流程
1. initComponent 日期、Dropdown、autocomplete
2. initListener
3. setState
4. showData


autocomplete
启用，del_flag=0
canedit (render:input.data("typeahead").selectVlue = data.TREATMENT_NAME;)
后台start, limit

dropdown
option:
{
  idKey : 'USER_ID',
  txtKey : 'EMPLOYEE_NAME'
  isNeedClear: false,
  isNeedAll: true,
}
SelectWJZSDropdownFirstItem
$("#consultType").SetWJZSDropdownSelectedData(_data.CONSULT_TYPE_ID);
name .val()
id .attr('val')
禁用数据问题

## 绑定
input[data-name="stocktakeItemId"]
class="stocktakeItemId"
clone
模板（放在html还是js）
拼接 （不便于调试、修改样式，可以循环后直接html，提高性能，可以转单页应用）

[谈谈JavaScript中的双向数据绑定 - 每天学点javascript - 前端乱炖](http://www.html-js.com/article/Study-of-twoway-data-binding-JavaScript-talk-about-JavaScript-every-day?a=1&b=2)
[利用 JavaScript 数据绑定实现一个简单的 MVVM 库 - 我的前端开发总结 - SegmentFault](https://segmentfault.com/a/1190000004847657)

init:
datetimepicker today
dropdown SelectWJZSDropdownFirstItem

初始化控件

load:
id
input val
datetimepicker format
dropdown
特殊控件 setToothPosition
span text

store：
delFlag: $(ele).css("display") === "none" ? 1 : 0




diff view edit
1. 控件 input or span td
2. 校验
3.



## format
- number
- Date
- null undefined text
- 根据值确定样式

## save
- verify
- storeData
- save


content-inner 注意只有overflow的控制
IE8自己配置height

href="javascript:void(0);"
href="javascript:;"
href="#"

<div class="tab-nav clear nav-head fr" style="margin:10px;">
    <a id="nav_category" href="javascript:void(0)" class="selected" value="category">按类别统计</a>
    <a id="nav_doctor" href="javascript:" class="" value="doctor">按医生统计</a>
</div>
<div id="tab-nav" class="fr">
    <a href="javascript:;" class="fl current" value="category">按类别统计</a>
    <a href="javascript:;" class="fl" value="doctor">按医生统计</a>
</div>
.fr a {
  width: 100px;
  height: 28px;
  line-height: 28px;
  margin-left: 20px;
  border: 1px solid #dfdfdf;
  color: #a4a4a4;
  text-align: center;
  border-radius: 4px;
}
.fr .current {
  height: 30px;
  line-height: 30px;
  border: none;
  background: #69afde;
  color: #fff;
}

datetimepicker validate(required,date) 在IE上有bug
