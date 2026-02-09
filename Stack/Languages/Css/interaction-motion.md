- [skew() – skewX() – skewY()](#skew--skewx--skewy)
---
# skew() – skewX() – skewY()
```bash
Dùng để bẻ góc độ của các cạnh.
```
**Syn**
```bash
transform: skew(xdeg, ydeg);
```
**Ex**
```html
<div>skew 20deg</div>
<div>skew 20deg 20deg</div>
```
```css
div{
    display: inline-block;
}
div:nth-child(1){
    margin-left: 100px;
    width: 100px;
    height: 100px;
    background-color: #f00;
    transform: skew(20deg);
}
div:nth-child(2){
    margin-left: 100px;
    margin-top: 100px;
    width: 100px;
    height: 100px;
    background-color: #f00;
    transform: skew(20deg, 20deg);
}
```