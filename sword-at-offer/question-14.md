题目：输入一个整数数组，实现一个函数来调整该数组中数字的顺序，使得所有奇数位于数组的前半部分，所有偶数位于数组的后半部分

题解：
可以借鉴快排的思路，初始化一个头指针和尾指针，头指针向后寻找偶数，尾指针向前寻找奇数，两者找到后当头指针位于尾指针前面时进行交换。

```js
const reorderOddEven = arr => {
  if (arr.length <= 1) {
    return arr;
  }
  let head = 0;
  let tail = arr.length - 1;
  while (head < tail) {
    while ((arr[head] & 0x1) === 1 && head < tail) {
      head++;
    }
    while ((arr[tail] & 0x1) === 0 && head < tail) {
      tail--;
    }
    const temp = arr[head];
    arr[head] = arr[tail];
    arr[tail] = temp;
  }
  return arr;
}
```

扩展：如果改成把负数排在非负数前面怎么做？

题解：可以只改动比较函数这一块，单独把比较的逻辑抽出来，而排序的逻辑不用动，参考sort函数的compareFunction

```js
const reorder = compare => arr => {
  if (arr.length <= 1) {
    return arr;
  }
  let head = 0;
  let tail = arr.length - 1;
  while (head < tail) {
    while (compare(arr[head]) && head < tail) {
      head++;
    }
    while (!compare(arr[tail]) && head < tail) {
      tail--;
    }
    const temp = arr[head];
    arr[head] = arr[tail];
    arr[tail] = temp;
  }
  return arr;
}

const isOdd = num => {
  return (num & 0x1) === 1;
}

const reorderOddEven = reorder(isOdd);
```