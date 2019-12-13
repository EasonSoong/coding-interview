题目：输入数字n，按顺序打印出从1到最大的n位十进制数。比如输入3，则打印出1、2、3一直到999。

这道题看起来简单，似乎遍历一遍最大的n位数就可以，但实际上可能存在大数的问题，举个例子：在JavaScript中，Number类型是一个64位的浮点数，对于整数，根据ECMAScript标准的要求，JavaScript能表示并进行精确算术运算的整数范围为：正负2的53次方，也即从最小值-9007199254740992到最大值+9007199254740992之间的范围。

解题思路：

* 非递归解法：

模拟整数的加法，初始化一个数组，存储n位0，然后不停的加1，并进行输出，注意边界的判断即可

```JS
const print1ToMaxNDigit = function(n) {
    if (n <= 0) {
        return;
    }
    const numArr = new Array(n).fill(0);
    while (incrementBy1(numArr)) {
        printNumber(numArr);
    }
}

const printNumber = function(numArr) {
    let i = 0;
    while (i < numArr.length && numArr[i] === 0) {
        i++;
    }
    let res = '';
    for (; i < numArr.length; i++) {
        res += numArr[i];
    }
    console.log(res);
}

const incrementBy1 = function(numArr) {
    let carry = 0;
    for (let i = numArr.length - 1; i >= 0; i--) {
        let num;
        if (i === numArr.length -1) {
            num = numArr[i] + 1 + carry;
        } else {
            num = numArr[i] + carry;
        }
        if (num >= 10) {
            carry = 1;
            numArr[i] = 0;
        } else {
            carry = 0;
            numArr[i] = num
            break;
        }
    }
    if (carry === 1) {
        return false;
    }
    return true;
}

```

* 递归解法：

```js
const print1ToMaxNDigits = (n) => {
    if (n <= 0) {
        return;
    }
    const numArr = new Array(n).fill(0);
    for (let i = 0; i < 10; i++) {
        numArr[0] = i;
        print1ToMaxNdigitsRecursive(numArr, 1);
    }
}

const print1ToMaxNdigitsRecursive = (numArr, index) => {
    if (index >= numArr.length) {
        printNumber(numArr);
        return;
    }
    for (let i = 0; i < 10; i++) {
        numArr[index] = i;
        print1ToMaxNdigitsRecursive(numArr, index + 1);
    }
}

const printNumber = function(numArr) {
    let i = 0;
    while (i < numArr.length && numArr[i] === 0) {
        i++;
    }
    let res = '';
    for (; i < numArr.length; i++) {
        res += numArr[i];
    }
    console.log(res);
}

```