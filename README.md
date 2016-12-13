#
CSS + JS Clock

demo:
https://telsaiori.github.io/javascript_css_clock/index.html

javascript30:
https://javascript30.com


在最一開的時候如果直接用
```
transform: rotate(260deg)
```

##transform-origin
來旋轉時針的話,會得不到我們想要的效果,因為我們需要的是他以時鐘的正中心為中心點為準來旋轉,所以必須使用**transform-origin**設定中心軸
```
.hand {
width:50%;
height:6px;
background:black;
position: absolute;
top:50%;
transform-origin: 100%;
transform: rotate(90deg);
}
```

然後為了讓指針能夠很滑順的轉動,也需要設定轉場的時間
```
transition: all 0.5s;
```

##transition-timing-function
因會想要營造出指針再走的時候的抖動（？）感加入了
```
transition-timing-function: cubic-bezier(0.1, 2.7, 0.58, 1);
```

##setInterval
為了要讓時鐘會自動跑,我們先用console.log來看看她會不會自動顯出訊息
```
function setDate(){
console.log('hi');

}

setInterval(setDate, 1000)
```
這時候重新整理網頁會看到console裡面的hi一直在增加

setInterval和setTimeout
差別在前者會依指定的秒數重複去執行程式,而後者只會跑一次

##取得秒數 &轉換成指針該轉的角度
使用getseconds來取得現在的秒數
```
const secondHand = document.querySelector('.second-hand');
const hourHand = document.querySelector('.hour-hand');
const minHand = document.querySelector('.min-hand');
function setDate(){
const now = new Date();
const seconds = now.getSeconds();
const secondsDegrees = ((seconds / 60) * 360 + 90);
secondHand.style.transform = `rotate(${secondsDegrees}deg)`;
const hours = now.getHours();
const hoursDegrees = ((hours / 12) * 360 + 90);
hourHand.style.transform = `rotate(${hoursDegrees}deg)`;
const mins = now.getMinutes();
const minsDegrees = ((mins / 60) * 360 + 90);
minHand.style.transform = `rotate(${minsDegrees}deg)`;
}

setInterval(setDate, 1000)
```

旋轉角度需要+90是因為一開始我們設定預設是停在90度






