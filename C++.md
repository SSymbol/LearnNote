### include <unordered_set>
unordered_set是一种无序集合
unordered_set::insert
unordered_set::find
unordered_set::erase
其底层实现是Hash,只保留不重复的值

find的返回值是一个迭代器iterator，如果找到了会返回指向目标元素的迭代器，没找到会返回end()，所以有如下写法：
```
//leetcode 349 
class Solution {
public:
    vector<int> intersection(vector<int>& nums1, vector<int>& nums2) {  
        unordered_set<int> result_set;
        unordered_set<int> nums_set(nums1.begin(),nums1.end());
        for(int num : nums2) {
            if (nums_set.find(num) != nums_set.end()) {
            //发现nums2的元素在nums_set里有出现过
                result_set.insert(num);
            }
        }
        return vector<int>(result_set.begin(),result_set.end());
    }
};
```
