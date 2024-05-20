See [[Coding Exercises]]

![](https://lh3.googleusercontent.com/z2ZvvsHkLgj9NJE2WCSA8R9vrZ498L2G0FpsxsqbFdzlCvecQe3tMsb07qzDCzIMVSXVTgKYu5meKhwCcQjiHiI00wV1l9MbrT0J0V2eAcfO42eIODo4PYlFk5w7XEji8V1ulkV2kLuvbbCLL0BNgTA)

* Solution 1
```js
function plusMinus(arr) {
    let numberOfZero = [], numberOfPos = [], numberOfNeg = [];
    arr.forEach((number) => {
        if (number > 0) {
            numberOfPos.push(number);
        } else if (number < 0) {
            numberOfNeg.push(number)
        } else {
            numberOfZero.push(number)
        }
    })
    console.log((numberOfPos.length / arr.length).toFixed(6))
    console.log((numberOfNeg.length / arr.length).toFixed(6))
    console.log((numberOfZero.length / arr.length).toFixed(6))
}
```

* Solution 2