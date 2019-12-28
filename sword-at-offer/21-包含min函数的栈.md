题目：定义栈的数据结构，请在该类型实现一个能够得到栈的最小元素的min函数。在该栈中，调用min、push及pop的时间复杂度都是O(1)。

leetcode：https://leetcode.com/problems/min-stack/submissions/

题解：看到题目第一想法是用一个变量记录当前最小值就可以了，但是这里忽略了一种情况，当最小值的被弹出栈时，如何知道下一个最小值呢？这道题可以用一个辅助栈来解，每次在入栈一个新元素时，判断该元素是否是最小值，是的话则在辅助栈中入栈该最小值，否则入栈原先的最小值。

```js
/**
 * initialize your data structure here.
 */
var MinStack = function() {
  this.s1 = [];
  this.s2 = [];
};

/** 
 * @param {number} x
 * @return {void}
 */
MinStack.prototype.push = function(x) {
  this.s1.push(x);
  if (this.s2.length > 0) {
    if (this.s2[this.s2.length - 1] > x) {
      this.s2.push(x);
    } else {
      this.s2.push(this.s2[this.s2.length - 1]);
    }
  } else {
    this.s2.push(x);
  }
};

/**
 * @return {void}
 */
MinStack.prototype.pop = function() {
  const res = this.s1.pop();
  this.s2.pop();
  return res;
};

/**
 * @return {number}
 */
MinStack.prototype.top = function() {
  if (this.s1.length > 0) {
    return this.s1[this.s1.length - 1];
  }
  return 0;
};

/**
 * @return {number}
 */
MinStack.prototype.getMin = function() {
  if (this.s2.length > 0) {
    return this.s2[this.s2.length - 1];
  }
  return 0;
};

/** 
 * Your MinStack object will be instantiated and called as such:
 * var obj = new MinStack()
 * obj.push(x)
 * obj.pop()
 * var param_3 = obj.top()
 * var param_4 = obj.getMin()
 */
```