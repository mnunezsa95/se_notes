See [[Coding Exercises]]


**![](https://lh3.googleusercontent.com/gEN2tQijktFPywOUasONljjZ_hzXRkyjAoWHGbrfY-zGq5ZL-LPl6NxOaZ9WrS0tkoGfCQbJOTOfJKiEdCAOlmJh-_CVSpeEo2mNAEcXRaG_w4meYsXqJKIWQyKz3NdNcOOF3ZGPDT0OdAgJuaXULcg)

```js
function timeConversion(s) {
  let startOfString = Number(s.slice(0, 2));
  let minutesAndSeconds = s.slice(2, 8);

  if (s.includes("AM") && startOfString === 12) {
    let newTime = String(12 - startOfString) + "0".concat(minutesAndSeconds);
    return newTime;
  }
  if (s.includes("AM") && startOfString <= 10) {
    let newTime = "0" + String(startOfString).concat(minutesAndSeconds);
    return newTime;
  }
  if (s.includes("PM") && startOfString < 12) {
    let newTime = String(12 + startOfString).concat(minutesAndSeconds);
    return newTime;
  }
  if (s.includes("PM") && startOfString === 12) {
    let newTime = String(startOfString).concat(minutesAndSeconds);
    return newTime;
  }
}
```