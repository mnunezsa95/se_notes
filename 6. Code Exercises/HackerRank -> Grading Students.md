See [[Coding Exercises]]

**![](https://lh4.googleusercontent.com/JCzauWiDZmlGNDUHAo1jgrUx84mw3AWLR_eqxZzXRkGVwpUiPWo1FdUQp5PyciUG1AQRLVjVnhnJ8OaMAT2Zb3okVN360ib-GDo3dMyo5BqSiWqd21JvICIuPDIB5oqxAOrtVVwskq0O1tT02qEps38)
#### Solution 1: Using map
```js
function gradingStudents(grades) {
let finalGrade = grades.map((grade) => {
	return grade >= 38 && grade % 5 >= 3 ? grade - (grade % 5) + 5 : grade;
});
	return finalGrade;
}
```