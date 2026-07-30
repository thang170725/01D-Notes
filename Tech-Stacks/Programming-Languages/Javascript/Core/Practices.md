# Time
## đồng hồ bấm giờ
```js
let second = document.getElementById("seconds");
let minute = document.getElementById("minutes");
let count = 56;
let mis = 0;
function Minute(){
    if(count == "60"){
        count = 0;
        mis += 1;
        minute.innerHTML = mis;
    }
}
function TimeMath(){
    count++;
    if(count < 10){
        count = "0" + count;
    }
    second.innerHTML = count;
    Minute();
}
function main(){
    let res = setInterval(TimeMath, 1000)
    let but = document.getElementById("stop");
    but.onclick = function (){
        clearInterval(res);
    }
}
main()
```