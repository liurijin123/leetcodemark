# 实现 strStr() 函数。

给定一个 haystack 字符串和一个 needle 字符串，在 haystack 字符串中找出 needle 字符串出现的第一个位置 (从0开始)。如果不存在，则返回  -1。

**示例 1:**

输入: haystack = "hello", needle = "ll"
输出: 2

**示例 2:**

输入: haystack = "aaaaa", needle = "bba"
输出: -1
## 思路：
### 1、使用KMP算法

```
class Solution {
    public int strStr(String haystack, String needle) {
        if(needle.length()==0)return 0;
        int i=0;
        int j=0;
        int[] next = new int[needle.length()];
        getNext(needle,next);
        for (i = 0,j = 0; i < haystack.length(); ++i){
            while(j > 0 && haystack.charAt(i) != needle.charAt(j)){
                j = next[j-1];
            }
            if (haystack.charAt(i) == needle.charAt(j)){
                j++;
            }
            if (j == needle.length()){
               return i-j+1;
            }
        } 
        return -1;
    }
    public void getNext(String str,int[] next){
        int len = str.length();
        int k=0;
        next[0]=0;
        for(int i=1;i<len;i++){
            while(k>0 && str.charAt(k)!=str.charAt(i)){
                k=next[k-1];
            }
            if(str.charAt(k)==str.charAt(i)){
                k++;
            }
            next[i]=k;
        }
    }
}
```
