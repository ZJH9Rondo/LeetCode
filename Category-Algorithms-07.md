# LeetCode-Category-Algorithms-07

## Title
  * Reverse Integer

### Description
  * Reverse digits of an integer.
  * Here are some good questions to ask before coding. Bonus points for you if you have already thought through this!
  If the integer's last digit is 0, what should the output be? ie, cases such as 10, 100.
  Did you notice that the reversed integer might overflow? Assume the input is a 32-bit integer, then the reverse of 1000000003 overflows. How should you handle such cases?
  For the purpose of this problem, assume that your function returns 0 when the reversed integer overflows.

  * Example

    ```
        Example1: x = 123, return 321

        Example2: x = -123, return -321
    ```
### How can I solve the question
  * 首先，根据Description中的描述，这个题还是有坑的，第二条描述中提到了特殊的逆置之后如果首位是0应该怎么处理，还有就是在逆置过程中出现的整数溢出这个问题怎么解决？测试用例要求当出现整数溢出时默认返回0，不再进行后续操作。对于此类问题，由于以前写代码没考虑这些极端的问题(不然怎么会来刷LeetCode)，就不了解整数溢出的机制以及判断方法，去学习了整数溢出的相关东西，然后因为javascript实现，javascript原生对象Math附带的方法帮了大忙，在设置用于判断的max的时候要方便很多(具体见代码)，其余的部分就和普通的逆置没有区别了。


### Code
  * 我的实现
  * Runtime:135ms

  ```
        /**
      * @param {number} x
      * @return {number}
      */
      var reverse = function(x) {
          var result = 0,
              max = Math.floor(2147483647/10),
              firstData = 0,
              check = (x<0)?(-1) : 1;

          x = x*check;

          while(x !== 0){
             if(max < result || (result === max && x > 7)){
                 return 0;
             }
             firstData = x % 10;
             result = result*10 + firstData;
             x = Math.floor(x/10);
          }
          result = result*check;
          return result;
      };
  ```

  * 大牛实现
  * Runtime:129ms
  ```
        /**
      * @param {number} x
      * @return {number}
      */
      var reverse = function(x) {
        var negative = false;
        if (x < 0) {
            x = Math.abs(x);
            negative = true;
        }
        var ans = 0;

        while (x > 0) {
            ans = ans*10 + x % 10;
            x = Math.floor(x/10);
        }
        if (Math.abs(ans) > Math.pow(2,31) - 1) {
            return 0;
        }

        if (negative) {
            ans = ans * -1;
        }
        return ans;
      };
  ```

### 对比总结

#### 对比
    * 唯一的遗憾就是对Math的原生方法使用不够熟悉，没有想到直接用abs()和pow()方法
    
####　总结
   * 这道题学习了关于整数溢出的相关知识以及对Math()自带的方法熟悉了一遍
   * 关于整数溢出的相关知识可以看下面这篇文章，讲的很详细全面
    ```
      http://www.cnblogs.com/feisky/archive/2008/04/11/1586595.html
    ```
