---
title: JQuery & JQuery Plugin
date: 2017-03-27 11:31:57
categories:
- 前端
tags:
- Jquery
- front end
---

JQuery基础和JQuery相关插件的使用笔记。

## JQuery

### 关于jquery的一些事
>*有一次在公司无意间听到有人说“JQuery早就过时了，现在是Angular、Vue和React的天下了！”，JQuery真的过时了？*

我不得不承认Angular、Vue和React现在很火，而且是未来Web前端开发的趋势，但我并不是很同意这句话，为什么呢？
1. Angular、Vue和React是前端js框架，而JQuery我觉得只能把它算作是js的libray
2. JQuery一点都不过时，相反它在前端开发中扮演相当重要的角色。许多MVC框架中都默认加入了JQuery，比如Rails、YII2.0，还有那些基于JQuery的前端插件就更不必说了。
3. JQuery`马后炮`的特性,为什么说它是马后炮呢，因为它需要在DOM渲染成功后，才能会发挥作用。这个特性有时候会给我们带来很多麻烦，但有时候也可以帮我们完成MVVM无法完成的事情。

API参考文档: [JQuery API](http://www.php100.com/manual/jquery/index.html)

## Jquery UI

### 简介
jQuery UI包含了许多维持状态的小部件（Widget）

jQuery UI 主要分为3个部分：交互、微件和效果库。

1. 交互（Interactions）
交互部件是一些与鼠标交互相关的内容，包括缩放（Resizable） , 拖动（Draggable） , 放置（Droppable） , 选择（Selectable） , 排序（Sortable）等。
2. 小部件（Widgets）
主要是一些界面的扩展，包括折叠面板（Accordion） , 自动完成（Autocomplete） , 按钮（Button） , 日期选择器（Datepicker） , 对话框（Dialog） , 菜单（Menu） , 进度条（Progressbar） , 滑块（Slider） , 旋转器（Spinner） , 标签页（Tabs） , 工具提示框（Tooltip）等。

3. 效果库（Effects）
用于提供丰富的动画效果，让动画不再局限于jQuery的animate()方法。包括特效（Effect） , 显示（Show） , 隐藏（Hide） , 切换（Toggle） , 添加 Class（Add Class） , 移除 Class（Remove Class） , 切换 Class（Toggle Class） , 转换 Class（Switch Class） , 颜色动画（Color Animation）等。

官网API: [JQuery UI 1.10](http://api.jqueryui.com/1.10)
中文DEMO: [中文DEMO](http://www.jqueryui.org.cn/demo/5618.html)

### draggable
**拖动组件**

``` javascript
$( ".selector" ).draggable({
  ...
});
```

draggable demo: [DEMO](http://www.jqueryui.org.cn/demo/5611.html)

### droppable
**放置组件**

``` javascript
$( ".selector" ).droppable({
  ...
});
```

droppable demo: [DEMO](http://www.jqueryui.org.cn/demo/5622.html)

### sortable
**排序组件**

``` javascript
$( ".selector" ).sortable({
  ...
});
```

sortable demo: [DEMO](http://www.jqueryui.org.cn/demo/5643.html)

### draggable + droppable + sortable

``` javascript
$('.draggable').draggable
  helper: 'clone'
  zIndex: 9999
  scroll: true
  connectToSortable: '.droppable-wrap'

$('.droppable-wrap').droppable(
  accept: '.draggable'
).sortable(
  handle: '.title-wrap'
  items: '.question-wrap'
  axis: 'y'
  appendTo: 'parent'
  scroll: false
  receive: (event, ui) ->
    question_count++
    if ui.helper.context.id == 'singleselect'
      target = HandlebarsTemplates['questionnaires/select']({
        type: ui.helper.context.id,
        type_no: 1,
        index: question_count
      })
    if ui.helper.context.id == 'vote'
      target = HandlebarsTemplates['questionnaires/select']({
        type: ui.helper.context.id,
        type_no: 2,
        index: question_count
      })
    if ui.helper.context.id == 'multiselect'
      target = HandlebarsTemplates['questionnaires/select']({
        type: ui.helper.context.id,
        type_no: 3,
        index: question_count
      })
    if ui.helper.context.id == 'grade'
      target = HandlebarsTemplates['questionnaires/grade']({
        type: ui.helper.context.id,
        type_no: 4,
        index: question_count })
    if ui.helper.context.id == 'fill_in'
      target = HandlebarsTemplates['questionnaires/fill_in']({
        type: ui.helper.context.id,
        type_no: 5,
        index: question_count })
    $('.droppable-wrap').find('.draggable').before(target)
    $('.droppable-wrap').find('.draggable').remove()
  update: (event, ui) ->
    $('.no-question').remove()
    update_sort_no()
).disableSelection()
```
