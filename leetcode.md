1.两数之和

```python
class Solution:
    def twoSum(self, nums: List[int], target: int) -> List[int]:
        if not nums or len(nums) < 2:
            return []

        idx = dict()

        for i in range(len(nums)):
            remain = target - nums[i]
            if remain in idx:
                return [idx[remain], i]
            else:
                idx[nums[i]] = i
        return []
```



```c++
class Solution {
public:
    vector<int> twoSum(vector<int>& nums, int target) {
        unordered_map<int, int> hashtable; // 创建了一个无序映射（哈希表） hashtable，用于存储数组元素及其对应的索引。
        for (int i = 0; i < nums.size(); ++i) {
            auto it = hashtable.find(target - nums[i]);
            if (it != hashtable.end()) { // 如果找到了差值在哈希表中的索引，说明找到了两个数的组合，使得它们的和等于目标值。直接返回包含这两个索引的数组。
                return {it->second, i};
            }
            hashtable[nums[i]] = i;
        }
        return {};
    }
};
```

> `auto` 是 C++11 引入的关键字，用于自动推导变量的类型。它允许编译器根据变量的初始化表达式自动推断出变量的类型，从而简化代码书写，提高代码的可读性和可维护性。
>
> 在你提到的代码中，`auto` 关键字用于声明变量 `it`。这里的 `it` 是一个迭代器，它通过哈希表的 `find` 函数返回的结果进行自动推导。具体来说，`find` 函数返回一个迭代器，指向哈希表中关键字为 `target - nums[i]` 的元素，如果找到了该元素，否则返回哈希表的 `end()` 迭代器表示未找到。
>
> 使用 `auto` 的好处是你不需要显式地指定 `it` 的类型，而是让编译器自动推导出正确的类型。这样可以减少代码中的类型冗长，特别是在涉及复杂的数据结构时，代码更加简洁易读。