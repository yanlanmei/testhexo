$(document).ready(function() {
    //激活fullpage
    $('#fullpage').fullpage({
        //Navigation导航
        menu: '#menu',
        //锁定锚链接，链接不变化
        lockAnchors: false,
        //定义锚链接（使用active，设置页面默认）
        anchors:['firstPage', 'secondPage'],
        navigation: false,
        navigationPosition: 'right',
        navigationTooltips: ['firstSlide', 'secondSlide'],
        showActiveTooltip: false,
        slidesNavigation: true,
        slidesNavPosition: 'bottom',

        //Scrolling滚动
        //动画效果
        css3: true,
        //滚动的速度ms
        scrollingSpeed: 700,
        //插件滚动
        autoScrolling: true,
        fitToSection: true,
        fitToSectionDelay: 1000,
        //滚动条拖动
        scrollBar: false,
        easing: 'easeInOutCubic',
        easingcss3: 'ease',
        //底部滚动过度
        loopBottom: false,
        //顶部滚动过度
        loopTop: false,
        //幻灯片滚动过度
        loopHorizontal: true,
        continuousVertical: false,
        normalScrollElements: '#element1, .element2',
        scrollOverflow: false,
        touchSensitivity: 15,
        normalScrollElementTouchThreshold: 5,

        //Accessibility
        keyboardScrolling: true,
        animateAnchor: true,
        recordHistory: true,

        //Design设计
        //幻灯片箭头
        controlArrows: true,
        //页面内容水平垂直居中
        verticalCentered: true,
        //字体随窗口缩放
        resize : false,
        //页面颜色
        sectionsColor : ['#ccc', '#fff'],
        paddingTop: '3em',
        paddingBottom: '10px',
        //固定元素
        fixedElements: '#header, .footer',
        responsiveWidth: 0,
        responsiveHeight: 0,

        //Custom selectors
        sectionSelector: '.section',
        slideSelector: '.slide',

        //events
        onLeave: function(index, nextIndex, direction){},
        afterLoad: function(anchorLink, index){},
        afterRender: function(){},
        afterResize: function(){},
        afterSlideLoad: function(anchorLink, index, slideAnchor, slideIndex){},
        onSlideLeave: function(anchorLink, index, slideIndex, direction, nextSlideIndex){}
    });
});