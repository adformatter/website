---
layout: default
title:  Templating
---
<style>
.custom-element{
	text-decoration: none;
	display: flex;
	flex-direction: column;
	flex-wrap: wrap;
	box-sizing:border-box;
	color: #333333;
}
.text-element{
	padding: 5px;
}
.image-element{
	margin: 5px;
}
.af_image,
.el-image{
	background: #0054a5;
	background: -moz-linear-gradient(45deg,  #0054a5 0%, #207cca 50%, #2989d8 50%, #0054a5 100%); 
	background: -webkit-linear-gradient(45deg,  #0054a5 0%,#207cca 50%,#2989d8 50%,#0054a5 100%); 
	background: linear-gradient(45deg,  #0054a5 0%,#207cca 50%,#2989d8 50%,#0054a5 100%);
	text-align: center;
	justify-content: center;
	align-content: center;
	color: #FFFFFF; 
}
.af-ad-container{
	border: 1px solid #0054a5;
	box-sizing: border-box;
	position: relative;
	min-height: 75px;
	min-width: 75px;
}
.af-indicator{
	position: absolute;
    right: 0px;
    top: 0px;
    color: #FFFFFF;
    background-color: #0054a5;
    font-size: 10px;
    padding: 0px 3px 0px 5px;
    line-height: 16px;
}
.templating_demo{

}
#af_demo_single{

}
#af_demo_multiple{

}
#af_ad_multiple{
	align-content : space-around;
	justify-content : space-around;
}
#af_demo_subad{

}
#af_ad_subad{
	align-content : center;
	justify-content : center;
}
#af_ad_subad .image-element{
	margin: 0px;
}
.image-text{
	display: block;
}
.subad-text{
	display: block;
}
.el-heading{
	font-weight: 600;
	margin-top: 10px;
}
.el-subheading{
	font-weight: 500;
}
.el-content{
	font-size: 12px;
}

#af_demo_multiple .el-heading{
	color: #0054a5;
    background-color: rgb(247, 247, 247);
    border-color: #0054a5;
    border-bottom: 1px solid;
}
#af_demo_multiple .el-subheading{
	color: rgb(3, 201, 3);
    background-color: rgb(255, 255, 255);
    border-color: rgb(0, 0, 0);
}
#af_demo_multiple .el-content{
	color: #333333;
    background-color: rgb(255, 255, 255);
    border-color: rgb(0, 50, 0);
}

.af_demo_text{
	display: none;
}
.af_demo_image{
	/*display: none;*/
}
.af-tmpl-code pre{
  max-height: 300px;
}
</style>
#### Templating - ATE
adTemplate is similar to markdown but it will be in JSON format. adFormatter has **ATE** (Ad Template Engine) that renders the formatted ad. Below are the some of the examples of using ATE. 
<br>
#### Single plain ad
<div class="af-tmpl-code" id="af-tmpl-code1">
{% highlight javascript %}
template:{
  element:'ad-container',
  styles:{
    dimensions:[300, 100]
  },
  body:[{
    element:'image',
    data:'adImage',
    styles:{
      dimensions:[90, 90]
    }
  },{
    element:'container',
    styles:{
      dimensions:[180, 90]
    },
    body:[{
      element:'heading',
      data:'adHeading'
    },{
      element:'content',
      data:'adContent'
    }]
  }]
},
data:{
  ad:{
    id:'ad-Id',
    url:'advertiser-url.com'
  },
  adImage:'advertiser-url.com/ad-image',
  adHeading:'Image Text Ad Heading',
  adContent:'Content or Description for an Ad containing image and text.'
}
{% endhighlight %}
</div>
<img src="/img/single-ad.PNG" alt="" class="templating_demo af_demo_image" id="af_demo_image_single">
<div class="templating_demo af_demo_text" id="af_demo_text_single">
	<div class="af-ad-container" id="af_demo_single" style="width:300px;height:120px;">
		<div class="af-indicator">AF</div>
		<div class="custom-element container-element el-container" style="width:300px;height:120px;">
			<a href="http://g.com" class="custom-element image-element el-image" style="width:90px;height:100px;margin:10px">
				<span class="image-text">Image</span>
				<!-- <span class="subad-text">subAd</span> -->
			</a>
			<div class="custom-element container-element el-container" style="width:190px;height:100px;">
				<a href="http://g.com" class="custom-element text-element el-heading" style="">Image Text Ad Heading</a>
				<a href="http://g.com" class="custom-element text-element el-content" style="">Content or Description for an Ad containing image and text.</a>
			</div>
		</div>
	</div>
</div>
<br>
#### Ad having multiple ad elments and some color customization
<div class="af-tmpl-code" id="af-tmpl-code2">
{% highlight javascript %}
colorCombos:{
  // publisher or advertiser can set colors for 'text', 'background' and 'border'
  heading:[[0, 84, 165], [247, 247, 247], [0, 84, 165]],
  subheading:[[3, 201, 3], [255, 255, 255], [255, 255, 255]],
  content:[[51, 51, 51], [255, 255, 255], [255, 255, 255]]
}
template:{
  element:'container',
  data:'subAdData',
  styles:{
    dimensions:[180, 180]
  },
  group:{
    styles:{
      dimensions:[400, 400],
      flow:['row', 'auto', 'auto'],
      flowBreak:2
    }
  },
  body:[{
    element:'heading',
    data:'adHeading'
  },{
    element:'subheading',
    data:'adSubHeading'
  },{
    element:'content',
    data:'adContent'
  }]
},
data:{
  ad:{
    id:'ad-Id',
    url:'advertiser-url.com'
  },
  subAdData:[
    {
      adHeading:'heading1 multi text ad',
      adSubHeading:'subheading1 multi text ad',
      adContent:'content1 - This is a Text ad having multiple sub ad elements under single ad'
    },
    {
      adHeading:'heading2 multi text ad',
      adSubHeading:'subheading2 multi text ad',
      adContent:'content2 - This is a Text ad having multiple sub ad elements under single ad'
    },
    {
      adHeading:'heading3 multi text ad',
      adSubHeading:'subheading3 multi text ad',
      adContent:'content3 - This is a Text ad having multiple sub ad elements under single ad'
    },
    {
      adHeading:'heading4 multi text ad',
      adSubHeading:'subheading4 multi text ad',
      adContent:'content4 - This is a Text ad having multiple sub ad elements under single ad'
    }
  ]
}
{% endhighlight %}
</div>
<img src="/img/multi-ad.PNG" alt="" class="templating_demo af_demo_image" id="af_demo_image_multiple">
<div class="templating_demo af_demo_text" id="af_demo_text_multiple">
	<div class="af-ad-container" id="af_demo_multiple" style="width:430px;height:320px;">
		<div class="af-indicator">AF</div>
		<div class="custom-element container-element group-element" style="width:420px;height:320px;" id="af_ad_multiple" >
			<!-- <div class="column-break"></div> -->
			<div class="custom-element container-element el-container" style="width:190px;height:140px;">
				<a href="http://g.com" class="custom-element text-element el-heading" style="">heading1 multi text ad</a>
				<a href="http://g.com" class="custom-element text-element el-subheading" style="">subheading1 multi text ad</a>
				<a href="http://g.com" class="custom-element text-element el-content" style="">content1 - This is a Text ad having multiple sub ad elements under single ad</a>
			</div>
			<div class="custom-element container-element el-container" style="width:190px;height:140px;">
				<a href="http://g.com" class="custom-element text-element el-heading" style="">heading2 multi text ad</a>
				<a href="http://g.com" class="custom-element text-element el-subheading" style="">subheading2 multi text ad</a>
				<a href="http://g.com" class="custom-element text-element el-content" style="">content2 - This is a Text ad having multiple sub ad elements under single ad</a>
			</div>
			<!-- <div class="column-break"></div> -->
			<div class="custom-element container-element el-container" style="width:190px;height:140px;">
				<a href="http://g.com" class="custom-element text-element el-heading" style="">heading3 multi text ad</a>
				<a href="http://g.com" class="custom-element text-element el-subheading" style="">subheading3 multi text ad</a>
				<a href="http://g.com" class="custom-element text-element el-content" style="">content3 - This is a Text ad having multiple sub ad elements under single ad</a>
			</div>
			<div class="custom-element container-element el-container" style="width:190px;height:140px;">
				<a href="http://g.com" class="custom-element text-element el-heading" style="">heading4 multi text ad</a>
				<a href="http://g.com" class="custom-element text-element el-subheading" style="">subheading4 multi text ad</a>
				<a href="http://g.com" class="custom-element text-element el-content" style="">content4 - This is a Text ad having multiple sub ad elements under single ad</a>
			</div>
		</div>
	</div>
</div>
<br>
#### Ad having subAds
Some ads may contain subAds. Using adFormatter it is easy to configure these type of ads and also we can get subAd level viewability metrics
<div class="af-tmpl-code" id="af-tmpl-code3">
{% highlight javascript %}
template:{
  element:'container',
  styles:{
    dimensions:[400, 400],
    flowBreak:[1]
  },
  body:[{
    element:'image',
    subAd:true,
    data:'subAd1',
    styles:{
      dimensions:[180, 400]
    }
  },{
    element:'image',
    subAd:true,
    data:'subAd2',
    styles:{
      dimensions:[180, 180]
    }
  },{
    element:'image',
    subAd:true,
    data:'subAd3',
    styles:{
      dimensions:[180, 180]
    }
  }]
},
data:{
  ad:{
    id:'ad-Id'
  },
  subAd1:{
    subAd:{
      id:'subAd-Id1',
      url:'subAd-url1.com'
    },
    content:'subAd-url1.com/image'
  },
  subAd2:{
    subAd:{
      id:'subAd-Id2',
      url:'subAd-url2.com'
    },
    content:'subAd-url2.com/image'
  },
  subAd3:{
    subAd:{
      id:'subAd-Id3',
      url:'subAd-url3.com'
    },
    content:'subAd-url3.com/image'
  }
}
{% endhighlight %}
</div>
<img src="/img/sub-ad.PNG" alt="" class="templating_demo af_demo_image" id="af_demo_image_subad">
<div class="templating_demo af_demo_text" id="af_demo_text_subad">
	<div class="af-ad-container" id="af_demo_subad" style="width:430px;height:320px;">
		<div class="af-indicator">AF</div>
		<div class="custom-element container-element el-container" style="width:430px;height:320px;" id="af_ad_subad">
			<a href="http://g.com" class="custom-element image-element el-image" style="width:200px;height:285px;margin-right:15px">
				<span class="subad-text">subAd 1</span>
			</a>
			<a href="http://g.com" class="custom-element image-element el-image" style="width:170px;height:135px;margin-bottom:15px;">
				<span class="subad-text">subAd 2</span>
			</a>
			<a href="http://g.com" class="custom-element image-element el-image" style="width:170px;height:135px;">
				<span class="subad-text">subAd 3</span>
			</a>
		</div>
	</div>
</div>

<script>
	var flexDemos = document.querySelectorAll('.page-header')
	var flexSupported = false;
	var ftEl = document.createElement('span');
	ftEl.style.display = 'flex';
	if(ftEl.style.display == 'flex'){
		var windowWidth = 0;
		if (window.innerHeight) {
		    windowWidth = window.innerWidth;
		}else{
		    windowWidth = document.documentElement.clientWidth;
		}
		if(windowWidth >= 992){
			flexSupported = true;
		}
	}
	if(flexSupported == true){
		document.getElementById('af_demo_text_single').style.display = 'block';
		document.getElementById('af_demo_text_multiple').style.display = 'block';
		document.getElementById('af_demo_text_subad').style.display = 'block';
		document.getElementById('af_demo_image_single').style.display = 'none';
		document.getElementById('af_demo_image_multiple').style.display = 'none';
		document.getElementById('af_demo_image_subad').style.display = 'none';
	}
</script>