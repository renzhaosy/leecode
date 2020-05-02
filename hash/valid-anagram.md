# 有效的字母异位词

> 来源： [LeeCode 第 242 题](https://leetcode-cn.com/problems/valid-anagram)
> 难度： 中等
> 给定两个字符串 s 和 t ，编写一个函数来判断 t 是否是 s 的字母异位词。

示例  1:

输入: s = "anagram", t = "nagaram"
输出: true
示例 2:

输入: s = "rat", t = "car"
输出: false
说明:
你可以假设字符串只包含小写字母。

进阶:
如果输入字符串包含 unicode 字符怎么办？你能否调整你的解法来应对这种情况？

## 实现

遍历 s,利用 map 记录字母出现的次数，然后遍历 t,依次将 map 中的字母次数减少，最后当 map 为空的时候就说明 t 是 s 的异位词。

```js
/**
 * @param {string} s
 * @param {string} t
 * @return {boolean}
 */
var isAnagram = function(s, t) {
  if (s.length !== t.length) return false;
  if (s === t) return true;
  const map = {};
  for (let i = 0; i < s.length; i++) {
    map[s[i]] = (map[s[i]] || 0) + 1;
  }
  for (let k = 0; k < t.length; k++) {
    if (!map[t[k]]) {
      return false;
    } else {
      map[t[k]] = map[t[k]] - 1;
    }
  }
  for (let key in map) {
    if (map[key]) {
      return false;
    }
  }
  return true;
};
```
