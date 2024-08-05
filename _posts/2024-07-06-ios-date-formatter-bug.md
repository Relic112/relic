---
layout: post
title: 算法｜期末试题题解
categories: [算法]
description: iOS AddPP 的一个小 Bug，与 NSDateFormatter 有关。
keywords: 算法,C++
mermaid: false
sequence: false
flow: false
mathjax: false
mindmap: false
mindmap2: false
---
## 		算法设计考试题目解析

​													



### 1.贪婪法求解硬币问题（分值：20.00）

一个硬币系统中共有1、5、10、25、100共5种硬市，用贪婪法能否得到最优解？为什么？（提示：不能得到最优解，请举出反列，能得到最优解，请给出证明)

在一个包含1、5、10、25、100五种硬币的系统中，贪婪算法确实能得到最优解。这是因为这些硬币的面值具有某种特殊的性质，使得贪婪算法在这种情况下可以成功地找到最优解。



对于任意一个目标金额，贪婪算法选出的硬币组合是最优的，即硬币数量最少。可以通过以下步骤来验证：

1. **考虑基本情况：**

   - 对于金额1、5、10、25和100，显然贪婪算法只会选择一枚相应面值的硬币，这显然是最优解。
   - 对于金额小于5但大于1的情况，比如2、3和4，贪婪算法会选择相应数量的1分硬币，这也是最优解。

2. **构建一般情况：**

   对于一个任意的目标金额N（假设N为一个正整数），我们使用贪婪算法：

   - 假设N = 99。贪婪算法会首先选择一个100分的硬币，但这里没有大于99的情况，所以考虑N < 100的情况。
   - 对于N = 99，贪婪算法会首先选择3个25分硬币（总共75分），剩下24分，然后选择2个10分硬币（20分），剩下4分，最后选择4个1分硬币。

   这样，总共选择了3 + 2 + 4 = 9枚硬币。

3. **最优性验证：**

   我们需要证明不存在比上述方法更少硬币数的组合：

   - 假设存在比贪婪算法选出的硬币数更少的组合。我们称其为S。
   - S包含的总金额为N，即S的硬币总数目小于贪婪算法选出的硬币数。
   - 由于贪婪算法每次都选择最大的硬币面值，所以S中必定包含一些小面值的硬币，这些小面值的硬币数量和总金额都不能比贪婪算法选择的更少。

**数学归纳法证明**

为了进一步严谨地证明，我们可以用数学归纳法：

1. **基础情况：**
   - 当N = 1, 5, 10, 25, 100时，贪婪算法的解是显然最优的。
2. **归纳假设：**
   - 假设对于任意金额k (1 ≤ k ≤ N)，贪婪算法的解都是最优的。
3. **归纳步骤：**
   - 考虑金额N+1。贪婪算法会选择一个尽可能大的硬币面值，并对剩余的金额N+1 - d应用贪婪算法。根据归纳假设，对于N+1 - d的情况，贪婪算法是最优的，因此N+1也是最优的。





### 2.整数数组的重复项（分值：20.00）

【问题描述】删除有序数组中的重复项：给你一个升序排列的数组us,请你原地删除重复出现的
元素，使每个元素只出现一次，返回删除后数组的新长度。元素的相对顺序应该保持一致
【输入形式】112
【输出形式】2,12
【样例输入】112
【样例输出】2,12
【样例说明】函数应该返回新的长度2，并且原数组nums的前两个元素被修改为1,2。不需要考
虑数组中超出新长度后面的元素。
【评分标准】

 **解题步骤**

我们要删除有序数组中的重复项，使每个元素只出现一次，并返回删除后数组的新长度。原数组的元素顺序应该保持不变。

**1：理解题目**

给定一个升序排列的数组 `nums`，我们需要修改数组，使得每个元素只出现一次，并返回修改后的数组的新长度。我们不需要考虑数组中超出新长度后面的元素。

**2：分析问题**

由于数组是有序的，相同的元素必然是连续的。我们可以使用双指针技术来解决这个问题：

1. 使用一个指针 `i` 遍历整个数组。
2. 使用另一个指针 `j` 标记下一个唯一元素应放置的位置。

**3：逐步分析**

1. **初始检查**：如果数组为空，直接返回长度 0。

   ```cpp
   if (nums.empty()) return 0;
   ```

2. **初始化指针**：`j` 指针初始化为 1，因为第一个元素必定是唯一的。

   ```cpp
   int j = 1;
   ```

3. **遍历数组**：从第二个元素开始遍历数组。

   ```cpp
   for (int i = 1; i < nums.size(); ++i) {
   ```

4. **检查唯一元素**：如果当前元素 `nums[i]` 不等于前一个元素 `nums[i - 1]`，说明它是唯一的。

   ```cpp
   if (nums[i] != nums[i - 1]) {
       nums[j] = nums[i]; // 复制唯一元素
       ++j; // 移动指针
   }
   ```

5. **返回结果**：遍历结束后，`j` 就是新的数组长度。

   ```cpp
   return j;
   ```

**完整代码**

```c++
#include <iostream>
#include <vector>
using namespace std;

int removeDuplicates(vector<int>& nums) {
    if (nums.empty()) return 0;

    int j = 1; // 新数组的长度，及指向下一个放置唯一元素的位置
    for (int i = 1; i < nums.size(); ++i) {
        if (nums[i] != nums[i - 1]) {
            nums[j] = nums[i]; // 复制唯一元素
            ++j; // 移动指针
        }
    }
    return j; // 新的数组长度
}

int main() {
    int nums[ 100],k=0;
        char t;
	while(1){
    scanf("%d%c",&nums[k++],&t);
    if(t=='\n') break;
}
    int newLength = removeDuplicates(nums);
    cout << newLength << ",";
    for (int i = 0; i < newLength; ++i) {
        cout << nums[i];
        if (i < newLength - 1) cout << ",";
    }
    cout << endl;
    return 0;
}
```





### 3.动态规划算法解矩阵连乘(分值：20.00)

【问题描述】使用动态规划算法解矩阵连乘问题，具体来说就是，依据其递归式自底向上的方式进行计算，在计算过程中，保存子问题答案，每个子问题只解决一次，在后面计算需要时只要简单查一下得到其结果，从而避免大量的重复计算，最终得到多项式时间的算法。
【输入形式】在屏幕上输入第1个矩阵的行数和第1个矩阵到第个矩阵的列数，各数间都以一个空格分隔。
【输出形式】矩阵连乘A1.An的最少数乘次数
【样例1输入】
3035155102825
【样例1输出】
15125

**分析**

1. **定义子问题**：
   - 设 \(m[i][j]\) 为计算矩阵 \(A_i\) 到 \(A_j\) 的最少乘法次数。
   - 我们需要计算 \(m[1][n]\)。

2. **递归式**：
   - 设 \(Ai\) 到 \(Aj\) 的最优计算方式是先计算 \(Ai\) 到 \(Ak\) 和 \(Ak +1到Aj的两个结果相乘。递归式如下![image-20240614221239001](C:\Users\24938\AppData\Roaming\Typora\typora-user-images\image-20240614221239001.png)
   - 边界条件：当 \(i = j\) 时，m[i][j]= 0\)。

3. **表格计算**：
   - 使用一个二维数组 \(m\) 来保存子问题的答案。
   - 逐步计算 \(m[i][j]\) 的值，从小规模的问题开始，逐步解决大规模的问题。

**步骤详解**

1. **初始化输入：**

   - 读取矩阵的维度，构建数组 `p`。

     ```cpp
     int p[100];
     char t;
     while(1){
         scanf("%d%c",&p[k++],&t);
         if(t=='\n') break;
     }
     
     ```

2. **初始化矩阵 `m`：**

   - 矩阵 `m` 用于保存子问题的结果，初始化为 0。

     ```cpp
     vector<vector<int>> m(n + 1, vector<int>(n + 1, 0));
     ```

3. ***计算最优次序：**

   - 使用双重循环依次计算不同长度的子问题：

     ```cpp
     for (int length = 2; length <= n; ++length) {
         for (int i = 1; i <= n - length + 1; ++i) {
             int j = i + length - 1;
             m[i][j] = INT_MAX;
             for (int k = i; k < j; ++k) {
                 int q = m[i][k] + m[k + 1][j] + p[i - 1] * p[k] * p[j];
                 if (q < m[i][j]) {
                     m[i][j] = q;
                 }
             }
         }
     }
     ```

4. **输出结果：**

   - 最终结果保存在 `m[1][n]` 中。

     ```cpp
     cout << matrixChainOrder(p) << endl;
     ```

**完整代码**

```c++
#include <iostream>
#include <vector>
#include <climits>
using namespace std;

int matrixChainOrder(const vector<int>& p) {
    int n = p.size() - 1;
    vector<vector<int>> m(n + 1, vector<int>(n + 1, 0));

    for (int length = 2; length <= n; ++length) {
        for (int i = 1; i <= n - length + 1; ++i) {
            int j = i + length - 1;
            m[i][j] = INT_MAX;
            for (int k = i; k < j; ++k) {
                int q = m[i][k] + m[k + 1][j] + p[i - 1] * p[k] * p[j];
                if (q < m[i][j]) {
                    m[i][j] = q;
                }
            }
        }
    }
    return m[1][n];
}

int main() {
    int p[100];
	char t;
	while(1){
    scanf("%d%c",&p[k++],&t);
    if(t=='\n') break;
}
    cout << matrixChainOrder(p) << endl;
    return 0;
}
```





### 4.求编辑距离（分值：20.00）

【问题描述】求编辑距离：给定两个字符串word1和word2,返回将word1转换为word2所需的最
少操作次数。
【输入形式】
【输出形式】
【样例输入】"horse”"ros"
【样例输出】3
【样例说明】
horse->rorse(替换h'wih)
rorse->rose(删除r)
rose->ros(删除'e)



1. **定义状态**：
   - 设 `dp[i][j]` 为将字符串 `word1` 的前 `i` 个字符转换为 `word2` 的前 `j` 个字符所需的最少操作次数。

2. **状态转移方程**：
   - 如果 `word1[i-1] == word2[j-1]`，则 `dp[i][j] = dp[i-1][j-1]`。
   - 如果 `word1[i-1] != word2[j-1]`，则需要考虑三种操作：插入、删除和替换：
     \[
     dp[i][j] = \min(dp[i-1][j] + 1, \quad \text{(删除)} \\
     dp[i][j-1] + 1, \quad \text{(插入)} \\
     dp[i-1][j-1] + 1 \quad \text{(替换)})
     \]

3. **初始化**：
   - `dp[0][j] = j`，将空字符串转换为 `word2` 的前 `j` 个字符需要 `j` 次插入操作。
   - `dp[i][0] = i`，将 `word1` 的前 `i` 个字符转换为空字符串需要 `i` 次删除操作。

4. **结果**：
   - `dp[m][n]` 即为将 `word1` 完全转换为 `word2` 所需的最少操作次数，其中 `m` 是 `word1` 的长度，`n` 是 `word2` 的长度。

**步骤详解**

1. **初始化输入**：

   - `string word1 `, `word2 `;

2. **定义DP数组**：

   - `dp` 是一个二维数组，大小为 `(m+1) x (n+1)`，其中 `m` 是 `word1` 的长度，`n` 是 `word2` 的长度。

   ```cpp
   int m = word1.size();
   int n = word2.size();
   vector<vector<int>> dp(m + 1, vector<int>(n + 1, 0));
   ```

3. **初始化边界条件**：

   - 将空字符串转换为另一个字符串所需的操作次数。

   ```cpp
   for (int i = 0; i <= m; ++i) {
       dp[i][0] = i;
   }
   for (int j = 0; j <= n; ++j) {
       dp[0][j] = j;
   }
   ```

4. **计算状态转移**：

   - 对于每个 `i` 和 `j`，根据字符是否相同来计算 `dp[i][j]`。

   ```cpp
   for (int i = 1; i <= m; ++i) {
       for (int j = 1; j <= n; ++j) {
           if (word1[i - 1] == word2[j - 1]) {
               dp[i][j] = dp[i - 1][j - 1];
           } else {
               dp[i][j] = min({dp[i - 1][j] + 1,   // 删除
                               dp[i][j - 1] + 1,   // 插入
                               dp[i - 1][j - 1] + 1}); // 替换
           }
       }
   }
   ```

5. **返回结果**：

   - 最终的编辑距离存储在 `dp[m][n]` 中。

   ```cpp
   return dp[m][n];
   ```

完整代码

```c++
#include <iostream>
#include <vector>
#include <string>
#include <algorithm>
using namespace std;

int minDistance(string word1, string word2) {
    int m = word1.size();
    int n = word2.size();
    vector<vector<int>> dp(m + 1, vector<int>(n + 1, 0));

    for (int i = 0; i <= m; ++i) {
        dp[i][0] = i;
    }
    for (int j = 0; j <= n; ++j) {
        dp[0][j] = j;
    }

    for (int i = 1; i <= m; ++i) {
        for (int j = 1; j <= n; ++j) {
            if (word1[i - 1] == word2[j - 1]) {
                dp[i][j] = dp[i - 1][j - 1];
            } else {
                dp[i][j] = min({dp[i - 1][j] + 1,   // 删除
                                dp[i][j - 1] + 1,   // 插入
                                dp[i - 1][j - 1] + 1}); // 替换
            }
        }
    }

    return dp[m][n];
}

int main() {
    string word1 ;
    string word2 ;
    cin>>word1>>word2;
    cout << minDistance(word1, word2) << endl;
    return 0;
}
```





### 5.数组中的逆序对（分值：20.00）

【问题描述】
给定一个整数数组nums,返回数组中逆序对的数量。
逆序对是一对，j),其中：0<=i<j<nums.length和nums0>2*nums1.
【输入形式】
【输出形式】
【样例输入】1,3,2,3,1
【样例输出】2
【样例输入】2,4,3,5,1
【样例输出】3
【样例说明】
【评分标准】

步骤

1. **初始化**：我们创建一个二维动态规划表`dp`，其中`dp[i][j]`表示`word1`的前`i`个字符转换为`word2`的前`j`个字符所需的最小编辑距离。表的第一行和第一列分别初始化为从0到`m`（`word1`的长度）和从0到`n`（`word2`的长度）的自然数，表示通过删除或插入操作将空字符串转换为给定字符串所需的步骤数。
2. **填充动态规划表**：我们遍历`word1`和`word2`的所有字符，并比较它们。如果字符相同，则不需要进行任何操作，所以`dp[i][j] = dp[i - 1][j - 1]`。如果字符不同，则我们需要考虑三种操作：替换、删除和插入。替换操作对应于`dp[i - 1][j - 1] + 1`，删除操作对应于`dp[i - 1][j] + 1`，插入操作对应于`dp[i][j - 1] + 1`。我们选择这三种操作中的最小值，并加1（表示当前操作），作为`dp[i][j]`的值。
3. **返回结果**：最后，`dp[m][n]`将包含将`word1`转换为`word2`所需的最小编辑距离。我们返回这个值作为函数的结果。



首先，我们定义全局变量 `count` 来记录逆序对的数量，并声明 `merge` 和 `mergeSort` 函数的原型：

```cpp
#include <vector>  
#include <iostream>  
using namespace std;  
  
int count = 0; // 全局变量，记录逆序对数量  
  
// merge函数的声明  
void merge(vector<int>& nums, int left, int mid, int right);  
  
// mergeSort函数的声明  
void mergeSort(vector<int>& nums, int left, int right);  
  
int main() {  
    // ... (稍后在main函数中填充代码)  
    return 0;  
}
```

接下来，我们实现 `merge` 函数。这个函数负责合并两个已排序的子数组，并计算逆序对：

```cpp
void merge(vector<int>& nums, int left, int mid, int right) {  
    vector<int> temp(right - left + 1); // 创建临时数组  
    int i = left, j = mid + 1, k = 0;  
  
    // 合并两个有序子数组，并计算逆序对  
    while (i <= mid && j <= right) {  
        if ((long long)nums[i] <= 2LL * nums[j]) {  
            temp[k++] = nums[i++];  
        } else {  
            count += mid - i + 1; // 累加逆序对数量  
            temp[k++] = nums[j++];  
        }  
    }  
  
    // 将剩余元素添加到临时数组中  
    while (i <= mid) temp[k++] = nums[i++];  
    while (j <= right) temp[k++] = nums[j++];  
  
    // 将临时数组中的元素复制回原数组  
    for (i = left, k = 0; i <= right; ) {  
        nums[i++] = temp[k++];  
    }  
}
```

现在，我们实现 `mergeSort` 函数，这是一个递归函数，用于对数组进行归并排序：

```cpp
void mergeSort(vector<int>& nums, int left, int right) {  
    if (left >= right) return; // 递归结束条件  
    int mid = left + (right - left) / 2; // 找到中点  
    mergeSort(nums, left, mid); // 递归排序左半部分  
    mergeSort(nums, mid + 1, right); // 递归排序右半部分  
    merge(nums, left, mid, right); // 合并两个有序子数组  
}
```

最后，在 `main` 函数中，我们创建一个示例数组，调用 `mergeSort` 函数，并输出逆序对的数量：

```cpp
int main() {  
    int nums[100],k=0; 
    char t;
	while(1){
    scanf("%d%c",&nums[k++],&t);
    if(t=='\n') break;
}
    // 样例输入  
    mergeSort(nums, 0, nums.size() - 1); // 对数组进行归并排序并计算逆序对  
    cout << "Number of inverse pairs: " << count << endl; // 输出逆序对的数量  
    return 0;  
}
```


