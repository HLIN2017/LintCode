 
 
 
## Two Pointers (26)
**0. [Reverse Vowels of a String.java](https://github.com/awangdev/LintCode/blob/master/Java/Reverse%20Vowels%20of%20a%20String.java)**      Level: Easy      Tags: [String, Two Pointers]
      

vowels: 元音字母. 要求reverse所有元音字母.

##### 方法1: two pointer.
- 前后两个指针, 在while loop里面跑.
- 注意 i<j, 一旦相遇, 就break.
- 找到合适的, 就做swap.
- StringBuffer可以 sb.setCharAt()记得用.
- O(n)
##### 方法2:
拿出所有vowels, 反过来放进去. O(n)



---

**1. [2 Sum II - Input array is sorted.java](https://github.com/awangdev/LintCode/blob/master/Java/2%20Sum%20II%20-%20Input%20array%20is%20sorted.java)**      Level: Medium      Tags: [Array, Binary Search, Two Pointers]
      

升序array, 找2SUM.

#### 方法1:
- 排序好的array. Two pointer移动start和end，核查sum.
- 注意sum用long.
- O(n) time

#### 方法2: Binary Search, 因为已经排好序了啊
- 定住一个valueA, 然后在剩下的里面 binary serach 找 (target - valueB)
- O(nLogN), 就不写了



---

**2. [2 Sum II.java](https://github.com/awangdev/LintCode/blob/master/Java/2%20Sum%20II.java)**      Level: Medium      Tags: [Array, Binary Search, Two Pointers]
      

与 2sum II - input array is sorted类似. 都是sort array, 然后two pointer.

LintCode的题. 注意找的是greater/bigger than target。

由于给定条件允许O(nLogn):   
   sort
   two pointer

while里面two pointer移动。每次如果num[left]+num[right] > target，那么其中所有num[left++]的加上num[right]都>target.   
也就是,num[right]不动，计算加入挪动left能有多少组，那就是: right-left这么多。 全部加到count上去。     
然后right--.换个right去和前面的left部分作比较。



---

**3. [3 Sum Closest.java](https://github.com/awangdev/LintCode/blob/master/Java/3%20Sum%20Closest.java)**      Level: Medium      Tags: [Array, Two Pointers]
      

3Sum 的一种简单形式, 并且都没有找index, value, 而只是找个sum罢了.

double for loop。 2Sum只能用土办法 left/right 2 pointers。 O(n^2)

注意：check closest时候用long, 以免int不够用



---

**4. [3 Sum.java](https://github.com/awangdev/LintCode/blob/master/Java/3%20Sum.java)**      Level: Medium      Tags: [Array, Two Pointers]
      

方法1:
sort array, for loop + two pointer. O(n)
处理duplicate wthin triplets: 
如果最外圈的移动点i重复, 一直顺到结尾的最后一个再用.
如果是triplet内有重复, 用完start point, 移动到结尾.

Previous notes:
注意:   
   1. 找 value triplets, 多个结果。注意，并非找index。    
   2. 要升序, 第一层for loop 从最后一个元素挑起, 保证了顺序。    
   3. 去掉duplicate: check用过的同样的数字，都跳掉。不需要用同样的数字再计算一边已有结果。

步骤:   
   1. For loop 挑个数字A.    
   2. 2Sum 出一堆2个数字的结果    
   3. Cross match 步骤1里面的A.   

时间 O(n^2), 两个nested loop

另外, 还是可以用HashMap来做2Sum。稍微短点。还是要注意handle duplicates.




---

**5. [3 Sum Smaller.java](https://github.com/awangdev/LintCode/blob/master/Java/3%20Sum%20Smaller.java)**      Level: Medium      Tags: [Array, Two Pointers]
      

一般的O(n3)肯定不行。在此基础上优化。
发现j,k满足条件时候，(k - j)就是所有 sum <target的情况了。
而一旦>target, 又因为j不能后退，只能k--，那么问题就被锁定了. 这样可以做到O(n2)



---

**6. [Intersection of Two Arrays II.java](https://github.com/awangdev/LintCode/blob/master/Java/Intersection%20of%20Two%20Arrays%20II.java)**      Level: Easy      Tags: [Binary Search, Hash Table, Sort, Two Pointers]
      

方法1:
用HashMap: 存一个nums1, 再拿nums2 check against map. 时间/空间:O(n)

方法2:
Binary search? 需要array sorted. 否则时间O(nlogn)不值得.
[没做完, 有错]



---

**7. [Minimum Size Subarray Sum.java](https://github.com/awangdev/LintCode/blob/master/Java/Minimum%20Size%20Subarray%20Sum.java)**      Level: Medium      Tags: [Array, Binary Search, Two Pointers]
      

方法1:
2 pointer, O(n). 找subarray, start 或 end pointer，每次一格这样移动.

好的策略: 
1. 先找一个solution, 定住end. 
2. 然后移动start; 记录每个solution if occurs
3. 然后再移动end，往下找。

Note: 虽然一眼看上去是nested loop.但是分析后，发现其实就是按照end pointer移动的Loop。start每次移动一格。总体上，还是O(n)

方法2:
Double for loop, base i 每次只+1, 所以最后O(n^2)

方法3:
Binary Search, O(nLogN)
Not done yet



---

**8. [Longest Substring Without Repeating Characters.java](https://github.com/awangdev/LintCode/blob/master/Java/Longest%20Substring%20Without%20Repeating%20Characters.java)**      Level: Medium      Tags: [Hash Table, String, Two Pointers]
      

方法1:
Two Pointers
双指针: 从start开始遍历, 但是第一步是while loop来推进end; 直到推不动end, 然后start++
巧妙点: 因为end是外围variable, 在start的loop上, end不会重置;[star ~ end] 中间不需要重复计算.
最终可以O(n);

Previous verison of two pointers:
用两个pointer, head和i.
注意：head很可能被退回到很早的地方，比如abbbbbba,当遇到第二个a，head竟然变成了 head = 0+1 = 1.      
当然这是不对的，所以head要确保一直增长，不回溯

方法2:
   HashMap<Char, Integer>: <character, last occurance index>
   一旦有重复, rest map.
   没有重复时候, 不断map.put(), 然后求max值

问题: 每次reset map之后就开始从新从一个最早的index计算, 最坏情况是O(n^2):
'abcdef....xyza'




---

**9. [Minimum Window Substring.java](https://github.com/awangdev/LintCode/blob/master/Java/Minimum%20Window%20Substring.java)**      Level: Hard      Tags: [Hash Table, String, Two Pointers]
      

基本思想: 用个char[]存string的frequency. 然后2pointer, end走到底, 不断validate.
符合的就process as result candidate.

HashMap的做法比char[]写起来要复杂一点, 但是更generic



---

**10. [Linked List Cycle.java](https://github.com/awangdev/LintCode/blob/master/Java/Linked%20List%20Cycle.java)**      Level: Easy      Tags: [Linked List, Two Pointers]
      

O(1) sapce: 用快慢指针。一个跑.next, 一个跑.next.next。 总有一次，fast会因为cycle而追上slow。
那个时候其实slow.val = fast.val.

O(n) space: 用HashMap，一直add elements.  如果有重复，那么很显然是有Cycle


---

**11. [Remove Nth Node From End of List.java](https://github.com/awangdev/LintCode/blob/master/Java/Remove%20Nth%20Node%20From%20End%20of%20List.java)**      Level: Medium      Tags: [Linked List, Two Pointers]
      

O(n), one pace, no extra space
找到窗口, 然后平移, 最后pre 和 head之间 skip一个node就好.



---

**12. [Linked List Cycle II.java](https://github.com/awangdev/LintCode/blob/master/Java/Linked%20List%20Cycle%20II.java)**      Level: Medium      Tags: [Linked List, Two Pointers]
      

方法1:
快慢指针, O(1)space.

确认有cycle后, 其实是数学问题:
当head == slow.next时候， head就是cycle starting point.
也就是说，当slow 移动到了那个回溯点，slow.next那个点就刚好是head的那个点...

证明:
1. 假设慢指针走t步, 快指针走快一倍, 也就是2t.
2. 我们假设cycle的长度是Y, 而进入cycle之前的长度为X.
3. 假设慢指针走了m圈cycle, 而快指针走了n圈cycle之后, 两个pointer相遇.
4. 最终在Y cycle里面的K点相遇, 也就是两个指针都在这最后一圈里面走了K 步.
=> 
那么:
t = X + mY + K
2t = X + nY + K
整合公式:
X + K = (n - 2m)Y
这里的m和n不过是整数的跑圈数, 也就是说X和K加在一起, 总归是结束cycle. X 和 K 互补
=> 结论: 当slow/fast 指针在K点相遇后, 再走X步, 就到了cycle的起点, 也就是题目要求的起点.

方法2:
HashMap, O(n) space


---

**13. [Trapping Rain Water.java](https://github.com/awangdev/LintCode/blob/master/Java/Trapping%20Rain%20Water.java)**      Level: Hard      Tags: [Array, Stack, Two Pointers]
      

这道题目的方法比较多.
#### 方法1
Array, 维持一个左手最高墙array, 右手最高强array.
对于每个index而言, vertically 能存放的最大水柱, 就是靠左右最高墙决定的:
min(leftHighestWall, rightHighestWall) - currHeight.

#### 方法2
方法1上面的优化, two pointer, 还是找左边最高和右边最高. O(1) space.
利用到了方法3里面的想法一样: 整个structure是被中间的最高bar 二分天下:
左边按照maxLeft来计算, 右边按照maxRight来计算.

#### 方法3
2 Pointers， 双面夹击:
1. 找中间最高bar的index    
2. 两面往中心扫：每次加上（topBarIndex - currIndex）* (elevation from previous index).也就是每次加一个横条。    
3. 每次还要减去block自身的height

#### 方法4
主要想法和方法3一致: 在山坡下坡的基础上, 一直用stack堆积bottom. 
最后遇到上升之前, 此时bottom可以用来跟stack之前堆积的所有下坡index做比较, 算跟他们高度相差的积水.
用了stack记录下坡, 然后用个while loop一挖到底的想法非常棒.




---

**14. [Find the Duplicate Number.java](https://github.com/awangdev/LintCode/blob/master/Java/Find%20the%20Duplicate%20Number.java)**      Level: Medium      Tags: [Array, Binary Search, Two Pointers]
      

- 注意不要思维定式: 以为mid是index
- 这里mid其实是binary search on value [1, n] 的一个value.
- 再次用到validate() function

Time: O(nLogN)



---

**15. [Permutation in String.java](https://github.com/awangdev/LintCode/blob/master/Java/Permutation%20in%20String.java)**      Level: Medium      Tags: [Two Pointers]
      

#### Two Pointer
- 如果做s1的permudation, 时间复杂度是O(n!) 肯定不可以
- 这里用HashTable的做法 (因为26字母, 所以用int[26]简化) 来记录window内的 character count
- 如果window内的character count 相等, 那么就是permudation
- 更进一步优化: 找两个map相互对应, 不如用一个 int[26]: s1对遇到的character做加法, s2对遇到的character做减法
- two pointer 运用在 n1, n2 的把控; 以及 s2.charAt(i - n1) 这一步



---

**16. [Implement strStr().java](https://github.com/awangdev/LintCode/blob/master/Java/Implement%20strStr().java)**      Level: Easy      Tags: [String, Two Pointers]
      

给两个string A, B, 找一个 B 在 A 种的起始位置.

#### Two Pointer
- 找到B在A中的起始位置, 然后看一下从这个点开始的substring是否等于B就可以了
- 还挺多坑的, 这些可以帮助优化:
- 1. 当B是“”的时候，也就是能在A的其实位置找到B....index = 0.
- 2. edge condition: 如果 haystack.length() < needle.length() 的话, 必须错, return -1
- 3. 如果在某个index, A后面剩下的长度, 比B的长度短, 也是误解, return -1



---

**17. [Interleaving Positive and Negative Numbers.java](https://github.com/awangdev/LintCode/blob/master/Java/Interleaving%20Positive%20and%20Negative%20Numbers.java)**      Level: Medium      Tags: [Two Pointers]
      

给一串数组 有正负数. 重新排列, 让数组里面 正数 和 负数 相隔开. 原来的order无所谓

#### Two pointer
- 需要知道正负的位置, 所以排序 O(nlogN)
- 考虑: 正数多还是负数多的问题, 举栗子就看出来端倪了
- 然后Two Pointer, swap 
- Time O(nlogn), space O(n)

#### extra space
- 用extra O(n) space, 把正负分成两个list
- 然后分别按照index填回去
- time O(n). space O(n)
- 但是就么有用到Two pointer了



---

**18. [Merge Sorted Array.java](https://github.com/awangdev/LintCode/blob/master/Java/Merge%20Sorted%20Array.java)**      Level: Easy      Tags: [Array, Two Pointers]
      

给两个排好序的数组, merge. 其中一个数组nums1有多余的位置

#### Basics
- A够长，那么可以从A的尾部开始加新元素。     
- 注意，从尾部，是大数字优先排末尾的.  



---

**19. [Palindrome Linked List.java](https://github.com/awangdev/LintCode/blob/master/Java/Palindrome%20Linked%20List.java)**      Level: Easy      Tags: [Linked List, Two Pointers]
      

#### Reverse Linked List
- Palindrome概念很简单, 但是要在Linkde List random access坐标, 是很难得: 所以需要把一半 ListNode 翻转
- reverse linked list: 遍历接开头
- 用快慢指正找到mid point
- Time O(n), 而且不需要用额外的空间(只是调换半个list的内部顺序), 所以空间O(1)

#### Previous Note
- Palindrome都是要两边回溯相等
- linkedlist不能reverse iterating， 那么就reverse the list, 从中间开花作比较。



---

**20. [Valid Palindrome.java](https://github.com/awangdev/LintCode/blob/master/Java/Valid%20Palindrome.java)**      Level: Easy      Tags: [String, Two Pointers]
      

验证string是不是 palindrome. 只考虑 alphanumeric, 其他字符可以忽略

#### Check Palindrome
- 前后两个指针, 往中间移动, 查看是否字母重合

#### 过滤 alphanumeric
- 可以用 ASCII code 来手动过滤, 只要 '0' ~ '9', 'a' ~ 'z', 'A' - 'Z' 之间的
- 也可以用 regular expression: match 所有这些字母, 是 [a-zA-Z0-9]
- 那凡是不是这些字母的 match, 就是取反: "[^a-zA-Z0-9]". 测试: https://regex101.com/



---

**21. [Remove Duplicates from Sorted Array.java](https://github.com/awangdev/LintCode/blob/master/Java/Remove%20Duplicates%20from%20Sorted%20Array.java)**      Level: Easy      Tags: [Array, Two Pointers]
      

给一个sorted array, 把重复的去掉: 也就是把不重复的按照顺序贴上来, array末尾多余的位置无所谓.

return unique item 的长度.

#### Two Pointers
- sorted array, 重复元素都在一起
- Two pointers 其实也可以是一个 for loop pointer, 另一个 dynamic variable.
- track unique index
- skip duplicated items
- O(n)

#### 思考模式:
- Remove Duplicate from Array 不同于remove from linked list.
- LinkedList里面我们是最好不要动node.val的，直接把node去掉。
- 而array我们很难直接把node去掉，又不能用新array，那么就要：
- 把不重复的element一个个放到最前面。
- 这个思想跟merge two sorted array （其中一个后续非常长的array可以放下arr1,arr2） 类似。
- 就是找个不会事后mess up，不会去动得index,把满足条件的element 填进去。这样保证了in place.
- *反向思维*：remove duplicate, 实际上也是找unique elements, and insert into original array



---

**22. [Remove Duplicates from Sorted Array II.java](https://github.com/awangdev/LintCode/blob/master/Java/Remove%20Duplicates%20from%20Sorted%20Array%20II.java)**      Level: Medium      Tags: [Array, Two Pointers]
      

给一个sorted array, 把重复的去掉: 也就是把不重复的按照顺序贴上来, array末尾多余的位置无所谓.

最多可重复出元素的数量不超过2个. return unique item 的长度.

#### Two Pointers
- sorted array, 重复元素都在一起
- 跟 `Remove Duplicates from Sorted Array` 几乎一模一样, 只不过unique index现在可以 validate 2 位
- 其余一模一样, use index to track unique item; skip if duplicated for more than 2 times
- O(n) time, O(1) space
- 这里也可以真的用2个pointers 写while loop, 但是没有必要, 只是单纯地走一个for loop其实就足够.



---

**23. [Rotate List.java](https://github.com/awangdev/LintCode/blob/master/Java/Rotate%20List.java)**      Level: Medium      Tags: [Linked List, Two Pointers]
      

给一个single linked list, 右移k steps. k non-negative.

#### Linked List basics
- 记得用dummy.next来存head.
- 特殊: 这里k可能大于list总长. 写一写linked node 移动的步数, 然后 k = k % n.
- 找到newTail, newHead, 然后利用dummy, 换位子



---

**24. [Partition Array.java](https://github.com/awangdev/LintCode/blob/master/Java/Partition%20Array.java)**      Level: Medium      Tags: [Array, Quick Sort, Sort, Two Pointers]
      

给一串数字, 和 int k. 根据k的值partition array, 找到第一个i, nums[i] >= k.

#### Two Pointer
- Quick sort的基础. 
- Partition Array根据pivot把array分成两半。
- 从array两边开始缩进。while loop到遍历完。非常直白的implement。
- 注意low/high,或者叫start/end不要越边界
- O(n)
- 注意: 这里第二个inner while `while(low <= high && nums[high] >= pivot) {..}` 采用了 `nums[high] >= pivot`
- 原因是题目要找第一个nums[i] >= k, 也就是说, 即便是nums[i]==k也应该swap到前面去
- 这个跟quick sort 原题有一点点不一样.




---

**25. [Container With Most Water.java](https://github.com/awangdev/LintCode/blob/master/Java/Container%20With%20Most%20Water.java)**      Level: Medium      Tags: [Array, Two Pointers]
      

#### Two Pointers
- 木桶理论。盛水的最高取决于最低的那面墙。
- 左右两墙，往中间跑动。
- 另:若一面墙已经小于另外一面，就要移动，换掉矮墙（可能下一面更高，或更低)
- 但决不能换掉当下的高墙，因为低墙已经limit的盛水的上限，若高墙移动，导致两墙之间距离减少，就注定水量更少了。（弄啥来，不能缺心眼啊）



---

