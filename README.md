//给jquery原型添加方法 引用此插件需先引入jquery
$.fn.accordion=function (colors,minWidth) {
	//设置默认值宽度   默认值要写在后面
	var minWidth=minWidth||0;
	var colors=colors||[];
	//$(this)是调用这个方法的jq对象
	var boxWidth=$(this).width();
	var boxHeight=$(this).height();
	
	//最大宽度
	var $li=$(this).find("li");
	
	var maxWidth=boxWidth-($li.length-1)*minWidth;
	
	var avgWidth=boxWidth/$li.length;
  
	//遍历li标签添加样式  li中只有颜色没有图片或背景图
	// $li.each(function(index,ele){
	// 	$(ele).css({backgroundColor:colors[index],width:avgWidth,height:boxHeight,float:"left"});
	// 	
	// });
  //如果想添加背景图 用这个
	$li.each(function(index,ele){
		$(ele).css({backgroundImage:colors[index],backgroundSize:"contain",width:avgWidth,height:boxHeight,float:"left"});
		
	});
	//li注册鼠标事件
	$li.on("mouseenter",function  () {
		$(this).stop().animate({width:maxWidth}).siblings().stop().animate({width:minWidth});
	});
	$li.on("mouseleave",function  () {
		$li.stop().animate({width:avgWidth});
	});
};
