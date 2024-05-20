See [[Coding Exercises]]

**![](https://lh4.googleusercontent.com/n9DS1sYUiESXen-op40Pv2It3v_HruoO8fwldVsqkfQDyxQ1KOEPkd578T2ueVOmjPCGfz2_RhLfKunjUVmBU6P30_NqMsI4mDNt6k-uXA6pilI6V8nBcq-Wn29qxCT-5nekynBtv_SDE9untcPhlcU)**

* Example 1
```js
function miniMaxSum(arr) {
    const maxNumber = Math.max(...arr);
    const minNumber = Math.min(...arr);
    const totalValue = arr.reduce((acc, cur) => {
        return (acc + cur) 
    }, 0);
    console.log((totalValue - maxNumber), (totalValue - minNumber))
}
```