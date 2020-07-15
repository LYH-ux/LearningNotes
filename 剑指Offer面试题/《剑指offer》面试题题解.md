# 剑指《offer》面试题

### 面试题4

在一个 n * m 的二维数组中，每一行都按照从左到右递增的顺序排序，每一列都按照从上到下递增的顺序排序。请完成一个函数，输入这样的一个二维数组和一个整数，判断数组中是否含有该整数。

示例:

现有矩阵 matrix 如下：

[
  [1,   4,  7, 11, 15],
  [2,   5,  8, 12, 19],
  [3,   6,  9, 16, 22],
  [10, 13, 14, 17, 24],
  [18, 21, 23, 26, 30]
]

- 思路

  从右上角或左下角来缩小动态查找范围。不能从左上角或右下角来，会有重复区域

- 注意点

  - vector二维数组中求行与列

    ```
       int rows = matrix.size();
    
       int columns = matrix[0].size();
    ```

  - 特殊测试用例

    ```
    [] 5
    [[-5]]-5
    ```

  - 易错点：忽略了判断条件中的边界

    ```
    while ( (row <= (rows-1) ) && column >= 0 )
    ```

- 题解

  ```
   bool findNumberIn2DArray(vector<vector<int>>& matrix, int target) {
          if(matrix.size() <= 0)
          {
              return false;
          }
          int rows = matrix.size();
          int columns = matrix[0].size();
          int row = 0;
          int column = columns - 1;
          while ( (row <= (rows-1) ) && column >= 0 )
          {
              if ( matrix[row][column] > target )
              {
                  column -- ;
              }
              else if ( matrix[row][column] < target )
              {
                  row ++;
              }
              else if(matrix[row][column] == target )
              {
                  return true;
              }
          }
          return false;
      }
  ```

  

### 面试题5

请实现一个函数，把字符串 s 中的每个空格替换成"%20"。

示例 1：

输入：s = "We are happy."
输出："We%20are%20happy."

- 审题

  是原字符串替换还是新建字符串。 

  - 如果是原字符串替换，稍微复杂些，同时要考虑字符数组长度。

  - 如果是C++中string，且只是返回string对象而不考虑空间复杂度，可考虑用辅助字符串。从前到后遍历一遍即可。不用自己管理内存
  - 优先考虑时间复杂度和空间复杂度均低的解法，及 O(n) 和O(1)

- 注意点

  - string对象的长度如何求，新建的空string对象可直接赋任意长度吗？ 申请内存的操作在哪一环节完成？

    C++标准程序库中的string类，和char比较起来，du不必担心内存是否足够、字符串长度等等，作为一个类出现，可以把它看成是C++的基本数据类型。 一般使用string类型，必须包含头文件 <string>。#include <string>

    所以说string会自动管理内存。 但本质上，它扩容、插入时候一定涉及到了移动。也有效率问题。

  - 在string类之间进行复制没有什么问题。
    但是要拷贝到内存中时就要注意。一定要在string取出的长度上加1。
    如下
    char buf[256];
    std::string str = "1234567890";
    memcpy( buf, str.c_str(), str.length()+1 );
    这样才能拷贝到字符串的结束符‘0’。要不就拷贝不到。
    string的length函数只计算有效字符的长度。如同C中的strlen函数。

  - **C++ 求string类数组的长度(元素个数)**

    **sizeof(数组名) / sizeof(数组名[0])**

    整个数组的长度/第一个元素的长度(长度是固定的)

    sizeof其作用是返回一个对象或类型所占的内存字节数，在windows下string是28

    string 是一个类，它的类型长度是固定的，即sizeof大小是固定的，与字符串长度无关。 

    它的类实现中应该是有一个char*指针，指向具体的字符串。实际字符串长度是length= strlen(a)

- 题解

  ```
      string replaceSpace(string s) {
          if(s.empty())
          {
              return s;
          }
          int size = s.size();
          int count = 0;
          int i=0;
          while(s[i]!='\0')
          {
              if(s[i]==' ')
              {
                  count++;
              }
              i++;
          }
          s.resize(size+count*2+1); /*this statement can't ignore*/
          i = size;
          int j = size+count*2;
          while(i >= 0)
          {
              if(s[i] == ' ')
              {
                  s[j--]='0';
                  s[j--]='2';
                  s[j--]='%';
                  i--;
              }
              else
              {
                  s[j--]=s[i--];
              }
          }
          return s;
      }
  ```

  改进：双100%

  ```
      string replaceSpace(string s) {
          if(s.empty())
          {
              return s;
          }
          int length = s.size()-1;
          int count = 0;
          int i=0;
          for(i=0; i<=length; i++)
          {
              if(s[i]==' ')
              {
                  count++;
                  s+="00";
              }
          }
          i = length;
          int j = length+count*2;
          while(i >= 0)
          {
              if(s[i] == ' ')
              {
                  s[j--]='0';
                  s[j--]='2';
                  s[j--]='%';
                  i--;
              }
              else
              {
                  s[j--]=s[i--];
              }
          }
          return s;
      }
  ```

### 面试题6

输入一个链表的头节点，从尾到头反过来返回每个节点的值（用数组返回）。

**示例 1：**

```
输入：head = [1,3,2]
输出：[2,3,1]
```

- 思路

  - 利用栈，先遍历列表，入栈。 再出栈，压入vector。
  - 因为题目给了vector，可以遍压列表，压完vector后，反向遍历。
  - reverse法

- 这道题要关注vector的用法

- 题解

  ```
      vector<int> reversePrint(ListNode* head) {
          vector<int> printNode;
          if(head == NULL)
          {
              return printNode;
          }
          stack<int> s;
          while(head != NULL)
          {
              s.push(head->val);
              head = head->next;
          }
          while(!s.empty())
          {
              printNode.push_back(s.top());
              s.pop();
          }
          return printNode;
      }
  ```

  ```
      vector<int> reversePrint(ListNode* head) {
          vector<int> res;
          while(head){
              res.push_back(head->val);
              head = head->next;
          }
          reverse(res.begin(),res.end());
          return res;
      }
  ```

### 面试题7:重建二叉树

输入某二叉树的前序遍历和中序遍历的结果，请重建该二叉树。假设输入的前序遍历和中序遍历的结果中都不含重复的数字。 

例如，给出

前序遍历 preorder = [3,9,20,15,7]
中序遍历 inorder = [9,3,15,20,7]
返回如下的二叉树：

​    3

   / \
  9  20
    /  \
   15   7

- 思路

  - 找根结点
  - 递归。 与树有关的，递归好解决。  但是效率不是很高。
  - 利用vector的引用，免去新建vector.
  - 要判断preorder是否等于endpreorder。 即子树只有一个结点。 直接返回根结点。
  - **可考虑用栈，免去递归。**

- 特殊用例 ：  [] []

- 题解

  ```
  /**
   * Definition for a binary tree node.
   * struct TreeNode {
   *     int val;
   *     TreeNode *left;
   *     TreeNode *right;
   *     TreeNode(int x) : val(x), left(NULL), right(NULL) {}
   * };
   */
  class Solution {
  public:
      TreeNode* buildTree(vector<int>& preorder, vector<int>& inorder) {
          if(preorder.empty()|| inorder.empty() || preorder.size()!=inorder.size())
          {
              return NULL;
          }
          return reconstructionTree(preorder,inorder,0,0,preorder.size());
      }
      TreeNode* reconstructionTree(vector<int>& pre, vector<int>& inorder,int preindex,int inorindex,int length)
      {
  
          TreeNode *root = new TreeNode(pre[preindex]);
          int rootInorder = inorindex,count = 0;
          int leftlength = 0, rightlength = 0;
          while(inorder[rootInorder]!=pre[preindex] && count <length)
          {
              rootInorder++;
              count++;
          }
          if(count<length)
          {
              leftlength  = count;
              rightlength = length - 1 - leftlength;
          }
          else
          {
              return NULL;
          }
          if(leftlength > 0)
          {
              root->left = reconstructionTree(pre,inorder,preindex+1,inorindex,leftlength);
          }
          if(rightlength> 0)
          {
              root->right = reconstructionTree(pre,inorder,preindex+1+leftlength,rootInorder+1,rightlength);
          }
          return root;
      }
  };
  ```

  ```
  /**
   * Definition for a binary tree node.
   * struct TreeNode {
   *     int val;
   *     TreeNode *left;
   *     TreeNode *right;
   *     TreeNode(int x) : val(x), left(NULL), right(NULL) {}
   * };
   */
  class Solution {
  public:
      TreeNode* buildTree(vector<int>& preorder, vector<int>& inorder) {
          if(preorder.empty()|| inorder.empty() || preorder.size()!=inorder.size())
          {
              return NULL;
          }
          TreeNode* root = new TreeNode(preorder[0]);
          stack<TreeNode*> s;
          s.push(root);
          int index = 0;
          for(int i=1; i< preorder.size(); i++)
          {
              TreeNode* temp = s.top();
              if(temp->val != inorder[index])
              {
                  temp->left = new TreeNode(preorder[i]);
                  s.push(temp->left);
              }
              else
              {
                  while((!s.empty())&& (s.top()->val == inorder[index]))
                  {
                      temp = s.top();
                      s.pop();
                      index++;
                  }
                  temp->right = new TreeNode(preorder[i]);
                  s.push(temp->right);
              }
          }
          return root;
      }
  };
  ```

### 面谋题21：

输入一个整数数组，实现一个函数来调整该数组中数字的顺序，使得所有奇数位于数组的前半部分，所有偶数位于数组的后半部分。

示例：

输入：nums = [1,2,3,4]
输出：[1,3,2,4] 
注：[3,1,2,4] 也是正确的答案之一。

- 测试用例

  - []
  - [全奇]  [全偶]
  - [奇数序列过半]

- 解题思路与注意点

  - 首末相查， 前面查奇数，  末尾查偶数。 碰到不满足的对换。 复杂度为O(n)

    while循环自减时注意条件， 不能使i,j越界。所以每次需要判断

  - 遍历数组，把奇数从头开始逐步替换。

- 题解

  ```
   vector<int> exchange(vector<int>& nums) {
           if(nums.size() <= 1)
           {
               return nums;
           }
           int i=0;
           int j=nums.size()-1;
           for(int i=0;i<nums.size();i++)
           {
               while(nums[i]%2 != 0 && i<j)
               {
                   i++;
               }
               while(nums[j]%2 == 0 && j>i)
               {
                   j--;
               }
               if(j<=i)
               {
                   break;
               }
               int temp = nums[i];
               nums[i] = nums[j];
               nums[j--] = temp;
           }
           return nums;
      }
  ```

  ```
  class Solution {
  public:
      vector<int> exchange(vector<int>& nums) {
  
          int left = -1;
          for(int i = 0; i < nums.size(); ++i)
          {
              if(nums.at(i) % 2 != 0)   /* if( nums.at(i) & 1)*/
              {
                  swap(nums.at(i), nums.at(++left));
              }
          }
          
          return nums;
      }
  };
  ```

  

### 面试题22 链表中倒数第k个结点

输入一个链表，输出该链表中倒数第k个节点。为了符合大多数人的习惯，本题从1开始计数，即链表的尾节点是倒数第1个节点。例如，一个链表有6个节点，从头节点开始，它们的值依次是1、2、3、4、5、6。这个链表的倒数第3个节点是值为4的节点。

 

示例：

给定一个链表: 1->2->3->4->5, 和 k = 2.

返回链表 4->5.

- 思路

  双指针， 快指针先走k步

- 题解

  ```
      ListNode* getKthFromEnd(ListNode* head, int k) {
          if(head == NULL || head->next == NULL )
          {
              return head;
          }
          if(k<=0)
          {
              return NULL;
          }
  
          ListNode* pBefore = head;
          ListNode* pBehind = head;
  
          for(unsigned int i=1; i < k; ++i)
          {
              if(pBefore->next != NULL)
              {
                  pBefore = pBefore->next;
              }
              else
              {
                  return NULL;
              }
          }
          while(pBefore->next != NULL)
          {
              pBefore = pBefore->next;
              pBehind = pBehind->next;
          }
          return pBehind;
      }
  ```

### 面试题24 反转链表

定义一个函数，输入一个链表的头节点，反转该链表并输出反转后链表的头节点。

 示例:

输入: 1->2->3->4->5->NULL
输出: 5->4->3->2->1->NULL

- 题解

  ```
      ListNode* reverseList(ListNode* head) {
          if(head == NULL || head->next == NULL)
          {
              return head;
          }
          ListNode* pre = NULL;
          ListNode* cur = head;
          ListNode* next = NULL;
  
          while(cur!= NULL)
          {
              next = cur->next;
              cur -> next = pre;
              pre = cur;
              cur = next;
          }
          return pre;
      }
  ```

  

### 面试题25 合并两个排序的链表

输入两个递增排序的链表，合并这两个链表并使新链表中的节点仍然是递增排序的。

示例1：

输入：1->2->4, 1->3->4
输出：1->1->2->3->4->4

- 测试用例
  - [5]  [1,2,4]
  - [ null]  [ 1,2,3]
  - [2]  [1] 

- 题解

  - 我的原始思路

    ```
        ListNode* mergeTwoLists(ListNode* l1, ListNode* l2) {
            if(l1 == NULL && l2 == NULL)
            {
                return NULL;
            }
            else if(l1 == NULL)
            {
                return l2;
            }
            else if(l2 == NULL)
            {
                return l1;
            }
            ListNode *head = NULL;
            if(l1->val <= l2->val)
            {
                head = l1;
            }
            else
            {
                head = l2;
            }
            ListNode* h1 = NULL;
            ListNode* h2 = NULL;
    
            while(1)
            {
                while(l1->val <= l2-> val )
                {
                    h1 = l1;
                    l1 = l1->next;
                    if(l1 == NULL)
                    {
                        h1 -> next = l2;
                        return head;
                    }
                }
                if(h1!= NULL)
                {
                    h1 -> next = l2;
                }
                while(l2->val < l1->val )
                {
                    h2 = l2;
                    l2 = l2->next;
                    if(l2 == NULL)
                    {
                        h2 -> next = l1;
                        return head;
                    }
                }
                if(h2!= NULL)
                {
                    h2 -> next = l1;
                }
            }
            return head;
        }
    ```

    

  - 原始思路的精简版

    ```
        ListNode* mergeTwoLists(ListNode* l1, ListNode* l2) {
            ListNode *dummy = new ListNode (-1);
            ListNode *cur = dummy;
            while(l1 && l2)
            {
                if(l1->val < l2->val)
                {
                    cur->next = l1;
                    cur = cur->next;
                    l1 = l1->next;
                }
                else
                {
                    cur->next = l2;
                    cur = cur->next;
                    l2 = l2->next;
                }
            }
    
            if(l1) cur->next = l1;
            else cur->next = l2;
    
            return dummy->next;
        }
    ```

    

### 面试题26 在树中查找子树

输入两棵二叉树A和B，判断B是不是A的子结构。(约定空树不是任意一个树的子结构)

B是A的子结构， 即 A中有出现和B相同的结构和节点值。

例如:
给定的树 A:

​    3
   / \ 

  4   5
  / \
 1   2
给定的树 B：

   4 
  /
 1
返回 true，因为 B 与 A 的一个子树拥有相同的结构和节点值。

- 思路

  - 碰到树的问题，递归较简单。 但是效率不高
  - 要考虑好边界条件，检查空指针。 空指针是不能被访问的。
  - 递归查找左子树，右子树。

- 题解

  ```
      bool isSubStructure(TreeNode* A, TreeNode* B) {
          bool result = false;
          if(A!= NULL && B!=NULL)
          {
              if(A->val == B->val)
              {
                  result = DoesHaveTree2(A,B);
              }
              if(!result)
              {
                  result = isSubStructure(A->left,B);
              }
              if(!result)
              {
                  result = isSubStructure(A->right,B);
              }
          }
          return result;
  
      }
  
      bool DoesHaveTree2(TreeNode* A, TreeNode* B)
      {
          if(B== NULL)
          {
              return true;
          }
          if(A == NULL)
          {
              return false;
          }
          if(A->val != B->val)
          {
              return false;
          }
          return DoesHaveTree2(A->left,B->left)&&DoesHaveTree2(A->right,B->right);
      }
  ```

  ```
  class Solution {
  public:
      bool isSubStructure(TreeNode* A, TreeNode* B) {
          return (A&&B)&&(dfs(A,B)||isSubStructure(A->left,B)||isSubStructure(A->right,B));   
      }
      bool dfs(TreeNode* a, TreeNode* b)
      {
          if(!b)return true;
          if(!a)return false;
          if(a->val!=b->val)return false;
          return dfs(a->left,b->left)&&dfs(a->right,b->right); 
      }
  };
  ```

  

### 面谋题27. 二叉树的镜像

请完成一个函数，输入一个二叉树，该函数输出它的镜像。

例如输入：

​     4

   /   \
  2     7
 / \   / \
1   3 6   9
镜像输出：

​    4

   /   \
  7     2
 / \   / \
9   6 3   1

示例 1：

输入：root = [4,2,7,1,3,6,9]
输出：[4,7,2,9,6,3,1]

- 思路

  - 还是遍历，前序遍历，在每次遍历时如果存在左右结点，则交换。
  - 要注意，两个结点均为空时返回根。 但是**还要判断一个结点是否为空的情况**。 如果为空，则该结点不能再访问。

- 错误范例

  - 忽视了指针。 交换时没有用temp。 交换是错误的

    ```
            TreeNode *mirror = root;
            if(mirror -> left != NULL)
            {
                mirror->left = mirrorTree(root->right);
            }
            if(mirror->right != NULL)
            {
                mirror->right = mirrorTree(root->left);
            }
    ```

    上面代码中，mirror->left = root->left.  实际上发生的操作是：  A = B  ， B=A 。 这样交换是错误的。

    而且会报错

- 题解

  ```
      TreeNode* mirrorTree(TreeNode* root) {
          if(root == NULL)
          {
              return NULL;
          }
          if(root -> left == NULL && root-> right == NULL)
          {
              return root;
          }
  
          TreeNode* temp = root -> left;
          root -> left = root -> right;
          root -> right = temp;
          
          if(root -> left != NULL)
          {
              root->left = mirrorTree(root->left);
          }
          if(root->right != NULL)
          {
              root->right = mirrorTree(root->right);
          }
          return root;
      }
  ```

  

### 面试题28 对称的二叉树

请实现一个函数，用来判断一棵二叉树是不是对称的。如果一棵二叉树和它的镜像一样，那么它是对称的。

例如，二叉树 [1,2,2,3,4,4,3] 是对称的。

   1

   / \
  2   2
 / \ / \
3  4 4  3
但是下面这个 [1,2,2,null,3,null,3] 则不是镜像对称的:

   1

   / \
  2   2
   \   \
   3    3

- 思路

  用递归加遍历。  定义一个对称前序遍历，即遍历父结点，然后先遍历右节点，再遍历左结点。

  比较两个遍历的结果。 如果有不一致的地方，则返回FALSE 

- 题解

  ```
      bool isSymmetric(TreeNode* root) {
          if(root == NULL)
          {
              return true;
          }
          return isSymmetric(root,root);
          
      }
      bool isSymmetric(TreeNode* root1, TreeNode* root2)
      {
          if(root1 == NULL && root2 == NULL )
          {
              return true;
          }
          if(root1 == NULL || root2 == NULL)
          {
              return false;
          }
          if(root1->val != root2 -> val)
          {
              return false;
          }
          return isSymmetric(root1->left,root2->right)&&isSymmetric(root1->right,root2->left);
      }
  ```

  

### 面试题29  顺时针打印矩阵

输入一个矩阵，按照从外向里以顺时针的顺序依次打印出每一个数字。

示例 1：

输入：matrix = [[1,2,3],[4,5,6],[7,8,9]]
输出：[1,2,3,6,9,8,7,4,5]
示例 2：

输入：matrix = [[1,2,3,4],[5,6,7,8],[9,10,11,12]]
输出：[1,2,3,4,8,12,11,10,9,5,6,7]

- 思路

  通过图示找出特点

  - 每次打印的起点都是(i，i),循环结束的条件是  rows  > 2*start  && columns > 2*start
  - 整个打印分4步，第一步一定有，后三步根据坐标条件判断

- 题解

  ```
      vector<int> spiralOrder(vector<vector<int>>& matrix) {
          vector<int>  printSequence;
          if(matrix.empty())
          {
              return printSequence;
          }
  
          int rows = matrix.size();
          int colmuns = matrix[0].size();
  
          int start = 0;
          
          while( rows > 2*start && colmuns > 2*start )
          {
              int endX = colmuns -1 - start;
              int endY = rows -1 -start;
  
              for(int i =start ; i<= endX; ++i)
              {
                  printSequence.push_back(matrix[start][i]);
              }
              if(start < endY)
              {
                  for(int i=start+1; i<= endY; ++i)
                  {
                      printSequence.push_back(matrix[i][endX]);
                  }
              }
              if(start < endX && start < endY)
              {
                  for(int i=endX-1; i>=start;--i )
                  {
                      printSequence.push_back(matrix[endY][i]);
                  }
              }
              if(start < endX && start <endY -1)
              {
                  for(int i=endY-1; i>=start+1; --i)
                  {
                      printSequence.push_back(matrix[i][start]);
                  }
              }
              ++start;
          }
          return printSequence;
      }
  ```

  

### 面试题30  包含min函数的栈

定义栈的数据结构，请在该类型中实现一个能够得到栈的最小元素的 min 函数在该栈中，调用 min、push 及 pop 的时间复杂度都是 O(1)。

示例:

MinStack minStack = new MinStack();
minStack.push(-2);
minStack.push(0);
minStack.push(-3);
minStack.min();   --> 返回 -3.
minStack.pop();
minStack.top();      --> 返回 0.
minStack.min();   --> 返回 -2.

- 思路

  利用一个辅助栈，该辅助栈要与栈同步， 即元素个数相同。 出现最小值时最小值入栈，否则最小栈的栈顶元素再次压栈。 

  每次出栈时，最小值栈和主栈都要pop

- 注意事项

  要注意边界的判断。 比如，最小栈为空时， 直接压入元素作为栈顶元素。  这个条件要判断对，否则容易因pop空栈而导致内存访问错误。

- 题解

  ```
  class MinStack {
  public:
      /** initialize your data structure here. */
      MinStack() {
          minStack = new stack<int>;
          if(minStack == NULL)
          {
              return ;
          }
          Stack = new stack<int>;
          if(Stack == NULL)
          {
              return;
          }
          minValue = 0;
      }
      
      void push(int x) {
          if(x< INT_MIN || x> INT_MAX)
          {
              return ;
          }
          Stack->push(x);
          if(minStack->empty())
          {
              minStack->push(x);
          }
          else if(x <= minStack->top())
          {
              minStack->push(x);
          }
          else
          {
              minStack->push(minStack->top());
          }
  
      }
      
      void pop() {
          if(!Stack->empty())
          {
              Stack->pop();
              minStack->pop();
          }
      }
      
      int top() {
          return Stack->top();
      }
      
      int min() {
          return minStack->top();
      }
  private:
      stack<int> *minStack;
      stack<int> *Stack;
      int minValue;
  };
  
  ```

  