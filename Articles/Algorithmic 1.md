LeetCode 1:
Given an array of integers, return indices(index的复数) of the two numbers such that they add up to a specific target.You may assume that each input would have exactly one solution, and you may not use the same element twice.

Example:
    Given nums = [2, 7, 11, 15], target = 9,
    Because nums[0] + nums[1] = 2 + 7 = 9,
    return [0, 1].

**解题思路：**
如果使用暴力搜索（遍历所有的两个数字的组合，然后算其和，这样虽然节省了空间，但是时间复杂度高）的话，那么该算法的时间复杂度为O(n^2)。我们知道HashMap是常数级查找速度，所以我们可以利用HashMap来使时间复杂度由O(n^2)降低为O(n)。步骤大致为：先遍历一遍数组，建立 HashMap 映射，然后再遍历一遍，开始查找，找到则记录 index。

**C++解法1:**

```
class Solution {
public:
    vector<int> twoSum(vector<int>& nums, int target) {
        unordered_map<int, int> m;
        vector<int> result;
        for (int i = 0; i < nums.size(); ++i) {
            //向unordered_map类型的m中插入键值对
            m[nums[i]] = i;
        }
        for (int i = 0; i < nums.size(); ++i) {
            int t = target - nums[i];
            //count()返回要查找的key在map的所有key种的出现次数。因为此容器不允许重复，故count()只可能返回 1 或 0，即可判断此key是否存在。此外需要判断是否与当前索引重复。
            if (m.count(t) && m[t] != i) {
                //void push_back(const T& x):向量尾部增加一个元素X
                res.push_back(i);
                res.push_back(m[t]);
                break;
            }
        }
        return res;
    }
};

```
**C++解法2：**

```
class Solution {
public:
    vector<int> twoSum(vector<int>& nums, int target) {
        unordered_map<int, int> m;
        vector<int> result;
        for(int i = 0; i < nums.size(); i++) {
            if(m.find(target - nums[i]) == m.end()) {
                m[nums[i]] = i;
            }else {
                result.push_back(m[ target - nums[i] ]);
                result.push_back(i);
                break;
            }
        }
        return result;
    }
};
```

**Java解法1：**

```
class Solution {
    public int[] twoSum(int[] nums, int target) {
        HashMap<Integer, Integer> m = new HashMap<Integer, Integer>();
        int[] result = new int[2];
        for (int i = 0; i < nums.length; i++) {
            m.put(nums[i], i);
        }
        for(int i = 0; i < nums.length; i++) {
            int t = target - nums[i];
            if(m.containsKey(t) && m.get(t) != i) {
                result[0] = i;
                result[1] = m.get(t);
                break;
            }
        }
        return result;
    }
}
```

**Java解法2:**

```
class Solution {
    public int[] twoSum(int[] nums, int target) {
        HashMap<Integer, Integer> m = new HashMap<Integer, Integer>();
        int[] result = new int[2];
        for(int i = 0; i < nums.length; i++) {
            int t = target - nums[i];
            if(m.containsKey(t) && m.get(t) != i) {
                result[0] = i;
                result[1] = m.get(t);
                break;
            }else {
                m.put(nums[i], i);
            }
        }
        return result;
    }
}
```



***
Words or phrases:

* (1)indices   index的复数形式
* (2)assume    假设
* (3)exactly   准确地，确切地
***
C++语法：

* 向量（Vector）是一个封装了动态大小数组的顺序容器（Sequence Container）。
* Vector<类型>标识符(最大容量,初始所有值)
* vector(int nSize,const t& t):创建一个vector，元素个数为nSize,且值均为t
* unordered_map和map的不同点：如果需要内部元素自动排序，使用map，不需要排序使用unordered_map
***



