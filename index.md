# Leetcode notes
Reach me with ncdenaozi@outlook.com

Someone tells me that write these notes down will somehow give you effort to complete the whole leetcode list, I really feel impossible to complete all leetcode issues but anyway I will give it a try.


## 7. Reverse Integer
use brutal force to solve this method, note that there already exists a macro called INT_MAX and INT_MIN in cpp std library, or can use (1<<31)-1 as max count.
**really bad idea not to use a stack instead of a vector :<**


 int reverse(int x) {
        
        vector<int> digit;
        double result=0;
        
        int temp=x;
        while(temp/10!=0){
            digit.push_back(temp %10);
            temp=temp/10;
        }
        digit.push_back(temp);
        
        int highest_digit=digit.size()-1;
        for(int i=0;i<digit.size();i++){
            result+=digit[i]*pow(10,highest_digit-i);
        }
        
        if (result>INT_MAX or result<INT_MIN)
            return 0;
        else
            return result;
    }
    
    
## 9. Palindrome Number
use simple vector not stack. I thought vector may be easier to control with head&tail pointer because it is quite difficult to remember the number poped out of stack, probably need another memory list?
Speed is quite slow, optimal solution is that we only need to reverse half of the number, kind of tricky one.

bool isPalindrome(int x) {
        if(x<0)
            return false;
        
        vector<int> digit;
        int temp=x;
        while(temp/10!=0){
            digit.push_back(temp%10);
            temp/=10;
        }
        digit.push_back(temp);
        
        int start=0;
        int end=digit.size()-1;
        
        while(start<end){
            if(digit[start]!=digit[end])
                return false;
            else{
                start++;
                end--;
            }    
        }
        return true;
        }
    
## 13. Roman to Integer
A hashmap<char,int>. Note that normal ROMAN NUMBER is written in large-to-small but things like IV is actually small to large, so have a memory to locate the last ROMAN digit.
**Pity that leetcode need premium to unlock the standard solution.**

int romanToInt(string s) {
        unordered_map<char,int> mp={pair('I',1),pair('V',5),pair('X',10),pair('L',50),pair('C',100),pair('D',500),pair('M',1000)};
        int result=0;
        
        char memory;       
        for(int i=0;i<s.size();i++){
            if(mp[s[i]]>mp[memory])
                result-=2*mp[memory];
            result+=mp[s[i]];
            memory=s[i];
        }
        return result; 
    }
}; 

## 14. Longest Common Prefix
Brute force with a decoder-like program, just runs the whole comparison char by char.
standard solution is using **divide and conquer**, I like the idea but the implementation could be fussy.

string longestCommonPrefix(vector<string>& strs) {
        if(strs.size()==1)
            return strs[0];
        string result;
        int index=0;
        while(index<strs[0].size()){
            char temp=strs[0][index];
            for(auto i:strs){
                if(i[index]!=temp)
                    return result;    
            }
            if(temp!='\x00')
                result.push_back(temp);                
            index++;
        }
        return result;
    }
}; 
    
  


## 20. Valid Parentheses
I fail for the first time because I am thinking how can I deal with the right side parenthese in the stack. But then I found out that only left-side parentheses should be pushed into the stack and the right-side is only used as a comparison.
                                     
bool isValid(string s) {
       if(s.size()%2==1)
            return false;
        
        unordered_map<char,char> mp={pair('(',')'),pair('[',']'),pair('{','}')};
        
        stack<char> stk;
        char x;
        
        for(int i=0;i<s.size();i++){
            //left side
            if(s[i]=='(' or s[i]=='[' or s[i]=='{')
                stk.push(s[i]);
            else{
            //right side
                if(stk.size()==0)
                    return false;
                    
                switch(s[i]){
                    case ')':
                        x=stk.top();
                        stk.pop();
                        if(x!='(')
                            return false;
                        break;
                    case '}':
                        x=stk.top();
                        stk.pop();
                        if(x!='{')
                            return false;
                        break;
                    case ']':
                        x=stk.top();
                        stk.pop();
                        if(x!='[')
                            return false;
                        break;
                }
            }
        }
        if(stk.empty())
            return true;
        else
            return false;
}

## 21. Merge Two Sorted Lists
Merge sort approach, each time only look at two node.                                     
ListNode* mergeTwoLists(ListNode* l1, ListNode* l2) {
        ListNode* result=new ListNode(0);
        ListNode* head=result;
        
        while(l1 or l2){
            if(l1 and l2){
                if(l1->val<l2->val){
                    head->next=l1;
                    l1=l1->next;
                }else{
                    head->next=l2;
                    l2=l2->next;
                }
            }else if(l1){
                head->next=l1;
                l1=l1->next;
            }else if(l2){
                head->next=l2;
                l2=l2->next;
            }
            head=head->next;
        }
        
        result=result->next;
        return result;
    }                                     

## 26. Remove Duplicates from Sorted Array
Use std::vector.erase(vector.begin()+i) to delete one element from the space. Note that after delete operation, the position and the size both reduce itself so i-- is needed.
Speed is quite slow, standard solution is in JAVA.

    int removeDuplicates(vector<int>& nums) {
        for(int i=1;i<nums.size();i++){
            if(nums[i]<=nums[i-1]){
                nums.erase(nums.begin()+i);
                i--;
            }
        }
        return nums.size();
    }

## 27. Remove Element
Almost same as problem 26.

     int removeElement(vector<int>& nums, int val) {
        for(int i=0;i<nums.size();i++){
            if(nums[i]==val){
                nums.erase(nums.begin()+i);
                i--;
            }
        }
        return nums.size();
    }


## 28. implement strStr()
Use std::string.compare(int position, int length, string substring) and traverse the haystack, there is a lot of corner case so add a few conditions.
     
int strStr(string haystack, string needle) {
        if(needle.size()==0)
            return 0;
        
        if(haystack.size()<needle.size())
            return -1;
        
        for(int i=0;i<haystack.size();i++){
            if(haystack.compare(i,needle.size(),needle)==0)
                return i;
        }
        return -1;
    }


## 35. Search Insert Position
A simple binary search and output the lower bound for not-found result;
     
int searchInsert(vector<int>& nums, int target) {
        int start=0;
        int end=nums.size()-1;
        while(start<=end){
            int mid=(start+end)/2;
            if(nums[mid]==target)
                return mid;
            if(nums[mid]<target)
                start=mid+1;
            else
                end=mid-1;
        }
        return start; // only difference between the downside one instead of -1
    }
 
 ## 45. Jump Games II
 Dynamic programing, answer vector only updates when this index has not been updated before.
 int jump(vector<int>& nums) {
        if (nums.size()==1)
            return 0;
        vector<int> ans(nums.size());
        for(int i=0;i<nums.size();i++){
            int j=nums[i];
            for(int x=1;x<=j;x++){
                if(ans[i+x]==0)
                    ans[i+x]=ans[i]+1;
                
                if(i+x==nums.size()-1)
                    return ans[i+x];
            }  
        }
        return 0;
    }

 ##55. Jump Game
 Find all zero point in the whole vector, for each zero, browse beforehead if nums[j]>(i-j) then bypass this zero, else we find if this zero position is the head position of the total array. If it is head position then return true, else return false.
 bool canJump(vector<int>& nums) {
        if(nums[0]==0 and nums.size()!=1)
            return false;
        
        for(int i=1;i<nums.size();i++){
            if(nums[i]==0){
                for(int j=i-1;j>=0;j--){
                    if(nums[j]>(i-j))
                        break;
                    else if(j==0){
                        if(i==nums.size()-1)
                            return true;
                        else
                            return false;
                    } 
                }
            }
        }
        return true;
    }
 
 

## 704. Binary search
Almost same as simple binary search, the time complexity is O(logn) for already sorted array.

int search(vector<int>& nums, int target) {
        int left=0;
        int pivot=0;
        int right=nums.size()-1;
        while(left<=right){
            pivot=(left+right)/2; //pivot=left+(right-left)/2 can deal with integer overflow
            if (nums[pivot] == target ) return pivot;
            else if(nums[pivot] < target ) left=pivot+1;
            else if(nums[pivot] > target ) right=pivot-1;           
        }
        return -1;
    }

## 58. Length of Last Word
use two pointer to identify the space, right pointer is the rightmost first non-space char and left pointer is the rightmost near-right sapce char.

     int lengthOfLastWord(string s) {
        int right=s.size()-1;
        while(s[right]==' '){
            right--;
        }
        
        int left=right-1;
        while(left>=0){
            if(s[left]==' ')
                break;
            left--;
        }
        
        return right-left;
    }


## 66. Plus one
An idea of carryout, note that the last carryout means you need extra 1 added to the front of vector which is the first digits.

     vector<int> plusOne(vector<int>& digits) {
        int carryout=0;
        digits[digits.size()-1]++;
        for(int i=digits.size()-1;i>=0;i--){
            if(carryout==1){
                digits[i]++;
                carryout=0;
            }
            if(digits[i]==10){
                digits[i]=0;
                carryout=1;
            }
        }
        if(carryout==1){
            digits.insert(digits.begin(),1);
        }
        return digits;
    }


## 67. Add binary
define a single digit function to add one digit together.

char addTwoBinaryNumbers(char a, char b, int& carry){
        if(a == '0' && b == '0')
        {
            if(carry > 0){
                carry = 0;
                return '1';
            }
            return '0';
        }
        else if(a == '0' && b == '1' || a=='1' && b=='0'){
            if(carry > 0){
                carry = 1;
                return '0';
            }
            return '1';
        }
        else if(a=='1' && b == '1'){
            if(carry > 0){
                carry = 1;
                return '1';
            }
            carry = 1;
            return '0';
        }
        return '0';
    }
    
    string addBinary(string a, string b) {
        string result = "";
        int carry = 0;
        int i = a.length()-1, j = b.length()-1;
        while(i>=0 && j>=0){
            result = addTwoBinaryNumbers(a[i], b[j], carry) + result;
            i--;
            j--;
        }
        while(i>=0){
            result = addTwoBinaryNumbers(a[i], '0', carry) + result;
            i--;
        }
        while(j>=0){
            result = addTwoBinaryNumbers(b[j], '0', carry) + result;
            j--;
        }
        if(carry){
            carry = 0;
            result = '1' + result;
        }
        return result;
    }


## 69. Sqrt(X)
Like a mathematical induction method to increment and try.

int mySqrt(int x) {
        long i=0;
        while(1){
            if(i*i<x){
                i++;
            }else if(i*i==x){
                return i;
            }else if(i*i>x){
                return i-1;
            }
        }
    }


## 70. Climbing Stairs
iterative approach.

int climbStairs(int n) {
        if(n>1){
            return climbStairs(n-1)+climbStairs(n-2);
        }
        else if(n==1){
            return climbStairs(n-1);
        }
        else if(n==0){
            return 1;
        }
        else if(n<0){
            return 0;
        }
        
        return 0;
    }
                     
## 83. Remove Duplicates from Sorted List
Use a memory to store the last smaller node since the list is non-decreasing order. Special case is that the end of list but there is a equal between memory and temp you need to free memory->next.
                      
ListNode* deleteDuplicates(ListNode* head) {
        if(head==nullptr)
            return head;
        
        ListNode* temp=head;
        ListNode* memory=head;
        
        if(temp->next){
            temp=temp->next;
        }
        while(temp){
            if(temp->val > memory->val){
                memory->next=temp;
                memory=memory->next;
            }else if(temp->val==memory->val and temp->next==nullptr){
                memory->next=nullptr;
            }
            
            temp=temp->next;
        }
        return head;
    }                      

## 88. Merge Sorted Array
Use a easy approach to push the original array behind the inserted position.
 
 void merge(vector<int>& nums1, int m, vector<int>& nums2, int n) {
        for(int x:nums2){
            int i=0;
            while(i<m){
                if(x>=nums1[i])
                    i++;
                else
                    break;
            }
            
            for(int k=m-1;k>=i;k--){
                int temp=nums1[k];
                nums1[k+1]=temp;
                nums1[k]=-1;
            }
            
            nums1[i]=x;
            m++;
        }
    }
 
## 94. Binary Tree Inorder Traversal
Use reference to pass the vector parameter.
 
 void Traverse(TreeNode* &root, vector<int> &result){
        if(root->left)
            Traverse(root->left,result);
        result.push_back(root->val);
        if(root->right)
            Traverse(root->right,result);
    }
    
    vector<int> inorderTraversal(TreeNode* root) {
        vector<int> result;
        if(root==nullptr)
            return result;
        Traverse(root,result);
        return result;
    }
 
## 100. Same Tree
 Tricky method I think, there is a lot of corner case.
bool isSameTree(TreeNode* p, TreeNode* q) {
        if(p==nullptr and q==nullptr)
            return true;
        else if(p==nullptr || q==nullptr)
            return false;
        else if(p->val!=q->val)
            return false;
        else
            return isSameTree(p->right,q->right) and isSameTree(p->left,q->left);
    }
 
 
 ## 101. Symmetric Tree
 Iterative style, note that the condition should be in && relationship.
 bool check(TreeNode* &a,TreeNode* &b){
        if (a==nullptr || b==nullptr)
            return a==b;
        
        return a->val==b->val && check(a->left,b->right) && check(a->right,b->left);
    }
        
    bool isSymmetric(TreeNode* root) {
        if(root==nullptr)
            return true;
        return check(root->left,root->right);
    }

 ## 104. Maximum Depth of Binary Tree
 It is very silly that leetcode will refuse a ternary operation but only accept MAX() macro.
 
 int maxDepth(TreeNode* root) {
        if(root==nullptr)
            return 0;
        else{
            return max(maxDepth(root->left),maxDepth(root->right))+1;
        }
    }
 
 ## 108. Covert Sorted Array to Binary Tree
 Recursive Method, use left and right to control the recursive size.
 TreeNode* CreateTree(int l, int r, vector<int> &nums){
        if(l>r)
            return nullptr;
        
        int mid=(l+r)/2;
        TreeNode* node=new TreeNode(nums[mid]);
        node->left=CreateTree(l,mid-1, nums);
        node->right=CreateTree(mid+1,r, nums);
        return node;
    }
    
TreeNode* sortedArrayToBST(vector<int>& nums) {
        if(nums.size()==0)
            return nullptr;
        return CreateTree(0,nums.size()-1,nums);
}
 
 
 ## 110. Balanced Binary Tree
 a very clever/lazy approach, slow but effective. Note that !flag statement is used to improve performance.
 bool flag=true;
    int maxDepth(TreeNode* root) {
        if(root==nullptr || !flag)
            return 0;
        else{
            if(abs(maxDepth(root->left)-maxDepth(root->right))>1)
                flag=false;
            
            return max(maxDepth(root->left),maxDepth(root->right))+1;
        }
    }
bool isBalanced(TreeNode* root) {
        maxDepth(root);
        return flag;
    }
 
 
 ## 111. Minimum Depth of Binary Tree
 Need to focus the node without nullptr left.
 int minDepth(TreeNode* root) {
        if(root==nullptr)
            return 0;
        else if(root->left==nullptr)
            return 1+minDepth(root->right);
        else if(root->right==nullptr)
            return 1+minDepth(root->left);
        else
            return 1+min(minDepth(root->left),minDepth(root->right));
    }
 
 ## 112. Path Sum
 Iterative approach. 
 bool hasPathSum(TreeNode* root, int targetSum) {
        if(root==nullptr)
            return targetSum==0;       
return hasPathSum(root->left,targetSum-root->val) || hasPathSum(root->right,targetSum-root->val);
 
 
 ## 118. Pascal's Triangle
 Note the equation result[i][j]=result[i-1][j]+result[i-1][j+1].
 vector<vector<int>> generate(int numRows) {
        vector<vector<int>> result;
        result.push_back(vector<int>(1,1));
        for(int i=1;i<numRows;i++){
            vector<int> row;
            row.push_back(1);
            for(int j=0;j<i-1;j++){
                row.push_back(result[i-1][j]+result[i-1][j+1]);
            }
            row.push_back(1);
            result.push_back(row);
        }
        return result;
    }
 
 ## 119. Pascal's Triangle II
 Same as 118                                  
vector<int> getRow(int rowIndex) {
        vector<vector<int>> result;
        result.push_back(vector<int>(1,1));
        
        for(int i=1;i<=rowIndex;i++){
            vector<int> row;
            row.push_back(1);
            for(int j=0;j<i-1;j++){
                row.push_back(result[i-1][j]+result[i-1][j+1]);
            }
            row.push_back(1);
            result.push_back(row);
        }
        return result[rowIndex];
    }

## 121. Best Time to Buy and Sell Stock
O(n) Approach, find min point and after minpoint just compare the min_profit.
int maxProfit(vector<int>& prices) {
        int min_point=INT_MAX;
        int profit=0;
        for(int i=0;i<prices.size();i++){
            if(prices[i]<min_point){
                min_point=prices[i];
            }else{
                profit=max(profit,prices[i]-min_point);
            }
        }
        return profit;
    }

 
## 125. Valid Palindrome
Note that start==end||start==end+1 deals with both odd and even number cases.
bool isPalindrome(string s) {
        string s_2;
        for(auto i:s){
            if(i>='a' and i<='z')
                s_2+=i;
            else if(i>='A' and i<='Z')
                s_2+=i-('A'-'a');
            else if(i>='0' and i<='9')
                s_2+=i;
        }
        if(s_2.size()<=1)
            return true;
        int start=0;
        int end=s_2.size()-1;
        while(start<end){
            if(s_2[start]==s_2[end]){
                start++;
                end--;
            }else
                break;
        }        
        return start==end||start==end+1;
    }

## 136. Single Number
bitwise operation xor is used to identify the only number left.
int singleNumber(vector<int>& nums) {
        int result=0;
        for(auto i:nums){
            result^=i;
        }
        return result;
    }
       
## 141. Linked List Cycle
Use a sily approach to save the pointer address
Standard solution: A fast route with *2 speed and A slow route with normal speed, if it is a cycled list then these two route will meet again.
bool hasCycle(ListNode *head) {
        vector<ListNode*> ptr_vec;
        while(head){
            bool Contained=false;
            for(auto i:ptr_vec){
                if(i==head)
                    Contained=true;
            }
            if(Contained)
                return true;
            else
                ptr_vec.push_back(head);
            head=head->next;
        }
        return false;
    }
             
## 142. Linked List Cycle II
fast slow pointer approach.
ListNode *detectCycle(ListNode *head) {
        if(head==nullptr)
            return nullptr;
        
        ListNode* fast=head;
        ListNode* slow=head;
        int count=0;
        while(fast->next!=nullptr){
            fast=fast->next->next;
            slow=slow->next;
            count++;
            if(fast==nullptr)
                return nullptr;
            
            if(fast==slow){
                fast=head;
                while(fast!=slow){
                    fast=fast->next;
                    slow=slow->next;
                }
                return fast;
            }    
        }
        return nullptr;
    }             

## 144. Binary Tree Preorder Traversal
Tree preorder traversal, very simple iterative mode
void Traversal(TreeNode* root, vector<int> &result){
        if(root){
            result.push_back(root->val);
            Traversal(root->left,result);
            Traversal(root->right,result);
        }
    }
    
vector<int> preorderTraversal(TreeNode* root) {
        vector<int> result;
        Traversal(root,result);
        return result;
    }
             
## 145. Binary Tree Postorder Traversal
Same as above             
void Traversal(TreeNode* root, vector<int> &result){
        if(root){
            Traversal(root->left,result);
            Traversal(root->right,result);
            result.push_back(root->val);
        }
    }
    
    vector<int> postorderTraversal(TreeNode* root) {
        vector<int> result;
        Traversal(root,result);
        return result;
    }             

             
             
             
# TEMPLATE

Syntax highlighted code block

# Header 1
## Header 2
### Header 3

- Bulleted
- List

1. Numbered
2. List

**Bold** and _Italic_ and `Code` text

[Link](url) and ![Image](src)
