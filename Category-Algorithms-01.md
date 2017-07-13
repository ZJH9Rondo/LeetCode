# LeetCode-Category-Algorithms-01

## Title
* Two Sum

* Description
> Given an array of integers, return indices of the two numbers such that they add up to a specific target.
You may assume that each input would have exactly one solution, and you may not use the same element twice.
> Example
```
    Given nums = [2, 7, 11, 15], target = 9,

    Because nums[0] + nums[1] = 2 + 7 = 9,
    return [0, 1].
```

### How can I solve this question

  * 首先,根据Description中的描述，此问题目的在根据target的需要，从给定的Array中选出两个所求和与target相等的元素，将其下标放入一个数组中并返回
  * 限制条件
    > 假定每个输入只有一种满足的可能(降低了实现难度)

### Code
  * 语言: Javascript

  * 我的实现代码
  * Runtime: 199ms
  ```
        /**
      * @param {number[]} nums
      * @param {number} target
      * @return {number[]}
      */
      var twoSum = function(nums, target) {
        if(nums.length<=1){
            return false;
        }
        var number=[];
        for(var i=0;i<nums.length;i++){
            for(var j=i+1;j<nums.length;j++){
                if(nums[i]+nums[j]==target){
                    number.push(i,j);
                    return number;
                }
            }
        }
      };
  ```

  * 大牛实现
  * Runtime: 95ms
  ```
        /**
      * @param {number[]} nums
      * @param {number} target
      * @return {number[]}
      */
      var twoSum = function(nums, target) {
        var buff = {},
            i=0;
        for(;i<nums.length ; i++){
            if(nums[i] in buff){
                return [buff[nums[i]],i]
            }else{
                buff[target-nums[i]] = i;
            }   
        }
      };
  ```

### 对比总结

####  对比

    * 问题很简单，但是在实现方式上还是可以看出思考的差距，最优解的实现，由于当前问题只需要寻找任意一组解满足需求即可，所以最优解通过target减去输入数组的第一个元素，在剩下的未被检索的元素中去寻找任意一个满足需求的数组元素即可，而自身的实现用了一个最原始的办法，没有考虑到更复杂情况下的实现，大牛的解法只能说更切合题意，而且最小Runtime这个解答没有考虑一些非法数据，比如数组中只有一个元素的情况，并且题目也要求不使用同一元素两次，所以数组只有一个元素的情况必定为非法数据。

####  总结
    * 小问题的拓展性
    * 对非法数据的考虑
    * 如何实现需求并将Runtime降到最小(时间复杂度)
