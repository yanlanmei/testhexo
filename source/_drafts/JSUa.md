
## 判断浏览器为移动端

<script type="text/javascript">
    browserRedirect();  
    function browserRedirect(){
        var sUA = navigator.userAgent.toLowerCase();
        var bIsIpad = sUA.match(/ipad/i) == 'ipad';
        var bIsIphoneOs =  sUA.match(/iphone os/i) == 'iphone os';
        var bIsMidp = sUA.match(/midp/i) == 'midp';
        var bIsUc7 = sUA.match(/rv:1.2.3.4/i) == 'rv:1.2.3.4';
        var bIsUc = sUA.match(/ucweb/i) == 'ucweb';
        var bIsAndroid = sUA.match(/android/i) == 'android';
        var bIsCE = sUA.match(/windows ce/i) == 'windows ce';
        var bIsWM = sUA.match(/windows mobile/i) == 'windows mobile';

        if(bIsIpad || bIsIphoneOs || bIsMidp || bIsUc7 || bIsUc || bIsAndroid || bIsCE || bIsWM){
            //phone
        }else{
            //PC
        }
    }
</script>