# BLOG of Lianhao Xue

## Who am I?
- Lianhao Xue or written in simplified Chinese as 薛连昊
- Specialized in Embedded system and hardware-software system development
- Of course, I am familiar with C++, because a modest man can never master C++.
- Have a deep base in network and network devices, including FPGA development and sequential logics.
- Also an amateur photographer, travel and taking pictures.
- eveonline player.

## Where am I now?
New York, USA, but I was born and raised in Shanghai, China

## How to reach me?
- check my profile at linkedin link linkedin.com/in/lianhao-xue-078251220
- Or send me email at ncdenaozi@outlook.com, u decide!

Following will be recorded as my daily Leetcode step by step improvement, lets see if I can finish this lol

## Leetcode notes
Someone tells me that write these notes down will somehow give you effort to complete the whole leetcode list, I really feel impossible to complete all leetcode issues but anyway I will give it a try.

## 747. Largest Number At Least Twice of Others
```
int dominantIndex(vector<int>& nums) {
        int largest=INT_MIN;
        int index=-1;
        
        for(int i=0;i<nums.size();i++){
            if(nums[i]>largest){
                largest=nums[i];
                index=i;
            }
        }
        
        for(int x=0;x<nums.size();x++){
            if(nums[x]!=largest){
                if(largest<2*nums[x])
                    return -1;
            }
        }
        
        return index;
    }
```

## 334. Increasing Triplet Subsequence
O(n) approach, a is the smallest number and b is the current pivot that just large than a
```
bool increasingTriplet(vector<int>& nums) {
        int a = INT_MAX, b = INT_MAX;
        
        for(int i=0;i<nums.size();i++){
            if(nums[i] < a)
                a = nums[i];
            else if(a < nums[i] && nums[i] < b )
                b = nums[i];
            else if(a<nums[i] && b < nums[i])
                return true;
        }
        
        return false;
    }
```

## 1394. Find Lucky Integer in an Array
since there is contrains in lucky number, we define a stable sized array
```
int findLucky(vector<int>& arr) {
        int largest=-1;
        int frequency[501];
        for(int i=0;i<501;i++)
            frequency[i]=0;
        
        for(auto i:arr)
            frequency[i]++;
        
        for(int i=0;i<501;i++)
            if(frequency[i]!=0)
                if(frequency[i]==i)
                    largest=max(largest,i);
        
        return largest;
    }
```

## 1550. Three Consecutive Odds
simple and easy
```
bool threeConsecutiveOdds(vector<int>& arr) {
        if(arr.size()<3)
            return false;
        
        for(int i=0;i<arr.size()-2;i++){
            if(arr[i]%2==1 and arr[i+1]%2==1 and arr[i+2]%2==1)
                return true;
        }
        
        return false;
    }
```
## 783. Minimum Distance Between BST Nodes
```
int minDiffInBST(TreeNode* root) {
        if(root==nullptr)
            return INT_MAX;
        
        int distance=INT_MAX;
        
        if(!root->left and root->right){
            TreeNode* temp=root->right;
            while(temp->left)
                temp=temp->left;
            
            distance=temp->val-root->val;
            return min(distance,minDiffInBST(root->right));
        }
            
        else if(!root->right and root->left){
            TreeNode* temp=root->left;
            while(temp->right)
                temp=temp->right;
            
            distance=root->val-temp->val;
            return min(distance,minDiffInBST(root->left));
        }
            
        else if(root->left and root->right){
            TreeNode* rgt=root->right;
            while(rgt->left)
                rgt=rgt->left;
            
            TreeNode* lft=root->left;
            while(lft->right)
                lft=lft->right;
            
            
            distance=min(root->val-lft->val,rgt->val-root->val);
            return min(distance,min(minDiffInBST(root->right),minDiffInBST(root->left)));
        }
        else
            return INT_MAX;
            
        
    }
```

## 973. K Closest Points to Origin
there is a way to solve it in O(Nlogk) ways but using priority queue, i think this visited array idea is better because selection sort algorithm is used.
```
vector<vector<int>> kClosest(vector<vector<int>>& points, int K) {
        vector<vector<int>> result;
        
        vector<int> visited(points.size());
        
        while(K!=0){
            double smallest=INT_MAX;
            int index=0;
            for(int i=0;i<points.size();i++){
                if(visited[i]==0){
                    double distance=sqrt(points[i][0]*points[i][0]+points[i][1]*points[i][1]);
                    if(distance<smallest){
                        smallest=distance;
                        index=i;
                    }
                }    
            }
            visited[index]=1;
            
            result.push_back(points[index]);
            K--;
        }
        return result;
    }
```
### 134. Gas Station
```
int canCompleteCircuit(vector<int>& gas, vector<int>& cost) {
        if(gas.size()!=cost.size())
            return -1;
        
        int result=-1;
        int step=gas.size();
        
        for(int i=0;i<step;i++){
            if(gas[i]==0 and cost[i]==0){
                
            }
            else if(gas[i]>=cost[i]){
                int tank=gas[i];
                cout<<tank<<endl;
                int current=i;
                int next=(current+1)%step;
                while(next!=i){
                    if(tank<cost[current])
                        break;
                    else
                        tank=tank-cost[current]+gas[next];
                    current=next;
                    next=(current+1)%step;
                    if(tank<0)
                        break;
                }
                if(tank>=cost[current]){
                    result=i;
                    break;
                }
            }
        }
                
        return result;
    }
```


### 2023. Number of Pairs of Strings With Concatenation Equal to Target
O(n2) approach, brutal force
```
int numOfPairs(vector<string>& nums, string target) {
        int result=0;
        
        for(int i=0;i<nums.size();i++){
            for(int j=0;j<nums.size();j++){
                if(i!=j){
                    string temp=nums[i]+nums[j];
                        if(temp==target)
                            result++;
                }
            }
        }
        
        return result;
    }
```


### 832. Flipping an Image
image flipping, description is kinda clear and easy
```
vector<vector<int>> flipAndInvertImage(vector<vector<int>>& image) {
        vector<vector<int>> result1;
        vector<vector<int>> result2;
        
        for(vector<int> vec:image){
            vector<int> temp;
            for(int i=vec.size()-1;i>=0;i--){
                temp.push_back(vec[i]);
            }
            result1.push_back(temp);
        }
        
        for(vector<int> vec:result1){
            vector<int> temp;
            for(int i=0;i<vec.size();i++){
                temp.push_back(!vec[i]);
            }
            result2.push_back(temp);
        }
        
        return result2;
    }
```

### 171. Excel Sheet Column Number
brutal force and using hashmap, optimal lambda solution is [&](const char &i){ r = (r * 26) + (i - 64);}
```
int titleToNumber(string columnTitle) {
        unordered_map<char,int> mp;
        for(int i=0;i<26;i++)
            mp.insert(make_pair((char)'A'+i,i+1));
        
        int result=0;
        for(int i=0;i<columnTitle.size();i++){
            result+=pow(26,(columnTitle.size()-i-1))*mp[columnTitle[i]];
        }
            
            
        return result;
    }
```

### 1791. Find Center of Star Graph
count the ingress and outgress degree of any certain node, use a huge array to store the node degree count
```
int findCenter(vector<vector<int>>& edges) {
        int node[100001];
        for(int i=0;i<100001;i++)
            node[i]=0;
        
        for(auto v:edges){
            for(auto n:v){
                node[n]++;
            }    
        }
        int largest=0;
        int index=0;
        for(int x=0;x<100001;x++){
            if(largest<node[x]){
                largest=node[x];
                index=x;
            }
        }
        return index;
    }
```
### 1588. Sum of All Odd Length Subarrays
brutal force solution
```
int sumOddLengthSubarrays(vector<int>& arr) {
        int total_len=arr.size();
        vector<int> len;
        for(int i=1;i<=total_len;i=i+2){
            len.push_back(i);
        }
        
        int sum=0;
        for(auto x:len){
            for(int s=0;s+x-1<arr.size();s++){ //begin index of subarray
                int this_arr=0;
                for(int index=0;index<x;index++){
                    this_arr+=arr[s+index];
                }
                cout<<this_arr<<endl;
                sum+=this_arr;
            }
        }
        
        return sum;
    }
```

### 1952. Three Divisors
Need to implement a is_prime funcctiona to check whether the square root is also a prime.
```
bool isPrime(int n){
        if(n==2 or n==1)
            return true;
        
        for(float i=2;i*i<=n;i++){
            float d=(float)n/(float)i;
            if(d==(int)d)
                return false;
        }
        
        return true;
    }
    
    bool isThree(int n) {       
        if(n==2 or n==1)
            return false;
            
        for(int i=2;i*i<=n;i++){
            if(i*i==n){
                if(isPrime(i))
                    return true;
            }
        }
        return false;
    }
```

### 515. Find Largest Value in Each Tree Row
use a modified BFS and a control value queue.size to implement this same layer sense.
```
vector<int> largestValues(TreeNode* root) {
        vector<int> result;
        queue<TreeNode*> q;
        TreeNode* head=root;
        
        if(root==nullptr)
            return result;
        
        q.push(head);
        while(!q.empty()){
            int q_size=q.size();
            int largest=INT_MIN;
            for(int i=0;i<q_size;i++){
                TreeNode* temp=q.front();
                q.pop();
                largest=max(largest,temp->val);
                if(temp->left)
                    q.push(temp->left);
                if(temp->right)
                    q.push(temp->right); 
            }
            result.push_back(largest);
        }
        
        return result;
    }
```

### 1486. XOR Operation in an Array
very easy approach, initialize and calculate
```
int xorOperation(int n, int start) {
        vector<int> arr;
        for(int i=0;i<n;i++){
            arr.push_back(start+2*i);
        }
        
        if(arr.size()==1)
            return arr[0];
        
        int result=arr[0];
        for(int x=1;x<arr.size();x++){
            result=result^arr[x];
        }
        
        return result;
    }
```

### 506. Relative Ranks
use a hash map to store the ranking
```
vector<string> findRelativeRanks(vector<int>& score) {
        vector<string> result;
        int visited_size=score.size();
        bool visited[visited_size];
        for(int i=0;i<visited_size;i++)
            visited[i]=false;
        
        unordered_map<int,int> mp;
        
        int count=1;
        for(int j=0;j<score.size();j++){
            int current_max=INT_MIN;
            int index=-1;
            for(int i=0;i<score.size();i++){
                if(visited[i]==false){
                    if(score[i]>current_max){
                        index=i;
                        current_max=score[i];
                    }
                }
                
            }
            visited[index]=true;    
            mp[index]=count;
            count++;
        }
        
        for(int i=0;i<visited_size;i++){
            if(mp[i]==1)
                result.push_back("Gold Medal");
            else if(mp[i]==2)
                result.push_back("Silver Medal");
            else if(mp[i]==3)
                result.push_back("Bronze Medal");
            else
                result.push_back(to_string(mp[i]));
        }
        
        return result;   
    }
```

### 2095. Delete the Middle Node of a Linked List
traverse and delete, note that only need to count the previous node of middle point, and you always need to check corner cases.
```
ListNode* deleteMiddle(ListNode* head) {
        ListNode* count=head;
        int c=0;
        while(count){
            c++;
            count=count->next;
        }
        
        if(c==1)
            return nullptr;
        
        int middle=c/2;
        
        ListNode* start=head;
        while(middle>1){
            start=start->next;
            middle--;
        }
        if(start->next->next==nullptr)
            start->next=nullptr;
        else
            start->next=start->next->next;
        
        return head;
    }
```

### 1653. Minimum Deletions to Make String Balanced
the key idea is that to count the pairs of a b-a sequence.
```
int minimumDeletions(string s) {
        stack<char> stk;
        int count=0;
        stk.push(s[0]);
        for(int i=1;i<s.size();i++){
            if(stk.empty())
                stk.push(s[i]);
            else if(stk.top()=='b' and s[i]=='a'){
                count++;
                stk.pop();
            }else
                stk.push(s[i]);   
        }
        
        return count;
    }
```

### 451. Sort Characters By Frequency
using a hashmap to store frequency and a vector to store the unique char
```
string frequencySort(string s) {
        string result;
        unordered_map<char,int> mp;
        vector<char> alphabet;
        for(char x:s){
            mp[x]++;
            bool is_in=false;
            for(auto i:alphabet)
                if(i==x)
                    is_in=true;
            
            if(!is_in)
                alphabet.push_back(x);
        }
       
        while(!alphabet.empty()){
            int largest=0;
            int index=0;
            char c;
            for(int i=0;i<alphabet.size();i++){
                if(mp[alphabet[i]]>largest){
                    largest=mp[alphabet[i]];
                    index=i;
                    c=alphabet[i];
                }
            }
            int time=largest;
            
            alphabet.erase(alphabet.begin()+index);
                
            while(time>0){
                result+=c;
                time--;
            }
             
        }
        return result; 
    }
```

## 1137. N-th Tribonacci Number
easy dp solution.
```
int tribonacci(int n) {
        if(n==0)
            return 0;
        if(n==1)
            return 1;
        if(n==2)
            return 1;
            
        vector<int> dp(n+1);
        dp[0]=0;
        dp[1]=1;
        dp[2]=1;
        
        
        for(int i=3;i<n+1;i++){
            dp[i]=dp[i-1]+dp[i-2]+dp[i-3];
        }
        
        return dp[n];
    }
```

### 1807. Evaluate the Bracket Pairs of a String
using a map to store the translation dictionary and then using the char index in string to find the replacement location.
```
string evaluate(string s, vector<vector<string>>& knowledge) {
        unordered_map<string,string> mp;
        for(vector<string> one_pair:knowledge){
            mp[one_pair[0]]=one_pair[1];  
        }
        string result="";
        for(int i=0;i<s.size();i++){
            if(s[i]=='('){
                string temp="";
                while(i<s.size()){
                    i++;
                    if(s[i]==')')
                        break;
                    else
                        temp+=s[i];
                }
                if(mp.find(temp)==mp.end())
                    result+="?";
                else
                    result+=mp[temp];
            }else
                result+=s[i];
        }
        return result;
    }
```

### 1880. Check if Word Equals Summation of Two Words
quite easy to translate a string into a int
```
bool isSumEqual(string firstWord, string secondWord, string targetWord) {
        int firstnum=0;
        for(int i=0;i<firstWord.size();i++){
            firstnum+=(firstWord[i]-'a')*pow(10,firstWord.size()-i-1);
        }
        
        int secondnum=0;
        for(int i=0;i<secondWord.size();i++){
            secondnum+=(secondWord[i]-'a')*pow(10,secondWord.size()-i-1);
        }
        
        int targetnum=0;
        for(int i=0;i<targetWord.size();i++){
            targetnum+=(targetWord[i]-'a')*pow(10,targetWord.size()-i-1);
        }
        
        return (firstnum+secondnum)==targetnum;
    }
```

### 204. Count Primes
counting Primes only require up to sqrt(X).
int countPrimes(int n) {
        int count=0;
        for(int X=n-1;X>1;X--){
            bool isPrime=true;
            for(int i=2;i*i<=X;i++){
                if(X % i==0)
                    isPrime=false;
            }
            
            if(isPrime)
                count++;
        }
        
        return count;
    }

### 1295. Find Numbers with Even Number of Digits
```
int findNumbers(vector<int>& nums) {
        int count=0;
        for(auto i:nums){
            int temp=i;
            int digit=0;
            while(temp>0){
                digit++;
                temp=temp/10;
            }
            if(digit%2==0)
                count++;
        }
            
        return count;
    }
```

### 151. Reverse Words in a String
Read the total string into a stack and then form it into a string. 
Note: for the last element in stack you only need to pop it without adding a space.
```
string reverseWords(string s) {
        stack<string> stk;
        string temp;
        for(int i=0;i<s.size();i++){
            if(s[i]!=' ')
                temp+=s[i];
            else{
                if(temp!=""){
                    stk.push(temp);
                    temp="";
                }
            }    
        }
        if(temp!=""){
            stk.push(temp);
            temp="";
        }
        
        string result;
        while(!stk.empty()){
            if(stk.size()>1){
                result+=stk.top();
                result+=' ';
                stk.pop();
            }else{
                result+=stk.top();
                stk.pop();
            }
        }
        
        return result;
    }
```

### 92. Reverse Linked List II
A very tricky solution that using stack to store the value, also it is hard to track the current position.
```
ListNode* reverseBetween(ListNode* head, int left, int right) {
        ListNode* result=head;
        ListNode* temp=head;
        stack<int> stk;
        int count=1;
        int count2=1;
        
        if(left>=right)
            return result;
        
        while(count<=right){
            if(count>=left)
                stk.push(temp->val);
            count++;
            temp=temp->next;
        }
        ListNode* buffer=temp;
        
        ListNode* traverse=head;
        while(count2<right){   
            if(count2>=left-1){
                if(!stk.empty()){
                    ListNode* node=new ListNode(stk.top());
                    stk.pop();
                    traverse->next=node;
                }
            }
            
            count2++;
            traverse=traverse->next;
        }
        traverse->next=buffer;
        
        return result;
    }
```

### 7. Reverse Integer
use brutal force to solve this method, note that there already exists a macro called INT_MAX and INT_MIN in cpp std library, or can use (1<<31)-1 as max count.
**really bad idea not to use a stack instead of a vector :<**
```
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
```    
    
### 9. Palindrome Number
use simple vector not stack. I thought vector may be easier to control with head&tail pointer because it is quite difficult to remember the number poped out of stack, probably need another memory list?
Speed is quite slow, optimal solution is that we only need to reverse half of the number, kind of tricky one.
```
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
```    
### 13. Roman to Integer
A hashmap<char,int>. Note that normal ROMAN NUMBER is written in large-to-small but things like IV is actually small to large, so have a memory to locate the last ROMAN digit.
**Pity that leetcode need premium to unlock the standard solution.**
```
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
```
### 14. Longest Common Prefix
Brute force with a decoder-like program, just runs the whole comparison char by char.
standard solution is using **divide and conquer**, I like the idea but the implementation could be fussy.
```
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
```   
### 20. Valid Parentheses
I fail for the first time because I am thinking how can I deal with the right side parenthese in the stack. But then I found out that only left-side parentheses should be pushed into the stack and the right-side is only used as a comparison.
```                                     
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
```
### 21. Merge Two Sorted Lists
Merge sort approach, each time only look at two node.                                     
```
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
```
### 26. Remove Duplicates from Sorted Array
Use std::vector.erase(vector.begin()+i) to delete one element from the space. Note that after delete operation, the position and the size both reduce itself so i-- is needed.
Speed is quite slow, standard solution is in JAVA.
```
int removeDuplicates(vector<int>& nums) {
        for(int i=1;i<nums.size();i++){
            if(nums[i]<=nums[i-1]){
                nums.erase(nums.begin()+i);
                i--;
            }
        }
        return nums.size();
    }
```
### 27. Remove Element
Almost same as problem 26.
```
     int removeElement(vector<int>& nums, int val) {
        for(int i=0;i<nums.size();i++){
            if(nums[i]==val){
                nums.erase(nums.begin()+i);
                i--;
            }
        }
        return nums.size();
    }
```

### 28. implement strStr()
Use std::string.compare(int position, int length, string substring) and traverse the haystack, there is a lot of corner case so add a few conditions.
```     
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
```

### 1822. Sign of the Product of an Array
count negative number
```
int arraySign(vector<int>& nums) {
        int negative=0;
        for(auto i:nums){
            if(i==0)
                return 0;
            if(i<0)
                negative++;
        }
        
        if(negative%2==1)
            return -1;
        else
            return 1;
    }
```

### 35. Search Insert Position
A simple binary search and output the lower bound for not-found result;
```     
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
``` 
### 45. Jump Games II
 Dynamic programing, answer vector only updates when this index has not been updated before.
 ```
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
```
### 55. Jump Game
Find all zero point in the whole vector, for each zero, browse beforehead if nums[j]>(i-j) then bypass this zero, else we find if this zero position is the head position of the total array. If it is head position then return true, else return false.
 ```
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
``` 
 
### 704. Binary search
Almost same as simple binary search, the time complexity is O(logn) for already sorted array.
```
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
```

### 58. Length of Last Word
use two pointer to identify the space, right pointer is the rightmost first non-space char and left pointer is the rightmost near-right sapce char.
```
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
```

### 66. Plus one
An idea of carryout, note that the last carryout means you need extra 1 added to the front of vector which is the first digits.
```
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
```

### 67. Add binary
define a single digit function to add one digit together.
```
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
```

### 69. Sqrt(X)
Like a mathematical induction method to increment and try.
```
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
```

### 70. Climbing Stairs
iterative approach.
```
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
```                     
### 83. Remove Duplicates from Sorted List
Use a memory to store the last smaller node since the list is non-decreasing order. Special case is that the end of list but there is a equal between memory and temp you need to free memory->next.
```                      
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
```
### 88. Merge Sorted Array
Use a easy approach to push the original array behind the inserted position.
``` 
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
 ```
### 94. Binary Tree Inorder Traversal
Use reference to pass the vector parameter.
``` 
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
``` 
### 100. Same Tree
 Tricky method I think, there is a lot of corner case.
 ```
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
``` 
 
 ### 101. Symmetric Tree
 Iterative style, note that the condition should be in && relationship.
 ```
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
```
 ### 104. Maximum Depth of Binary Tree
 It is very silly that leetcode will refuse a ternary operation but only accept MAX() macro.
``` 
 int maxDepth(TreeNode* root) {
        if(root==nullptr)
            return 0;
        else{
            return max(maxDepth(root->left),maxDepth(root->right))+1;
        }
    }
``` 
 ### 108. Covert Sorted Array to Binary Tree
 Recursive Method, use left and right to control the recursive size.
``` 
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
``` 
 
 ### 110. Balanced Binary Tree
 a very clever/lazy approach, slow but effective. Note that !flag statement is used to improve performance.
``` 
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
``` 
 
 ### 111. Minimum Depth of Binary Tree
 Need to focus the node without nullptr left.
``` 
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
``` 
 ### 112. Path Sum
 Iterative approach. 
``` 
 bool hasPathSum(TreeNode* root, int targetSum) {
        if(root==nullptr)
            return targetSum==0;       
return hasPathSum(root->left,targetSum-root->val) || hasPathSum(root->right,targetSum-root->val);
``` 
 
 ### 118. Pascal's Triangle
 Note the equation result[i][j]=result[i-1][j]+result[i-1][j+1].
``` 
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
 ```
 ### 119. Pascal's Triangle II
 Same as 118                                  
```
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
```
### 121. Best Time to Buy and Sell Stock
O(n) Approach, find min point and after minpoint just compare the min_profit.
```
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
```
 
### 125. Valid Palindrome
Note that start==end||start==end+1 deals with both odd and even number cases.
```
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
```

### 136. Single Number
bitwise operation xor is used to identify the only number left.
```
int singleNumber(vector<int>& nums) {
        int result=0;
        for(auto i:nums){
            result^=i;
        }
        return result;
    }
```       
### 141. Linked List Cycle
Use a sily approach to save the pointer address
Standard solution: A fast route with *2 speed and A slow route with normal speed, if it is a cycled list then these two route will meet again.
```
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
```             
### 142. Linked List Cycle II
fast slow pointer approach.
```
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
```
### 144. Binary Tree Preorder Traversal
Tree preorder traversal, very simple iterative mode
```
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
```             
### 145. Binary Tree Postorder Traversal
Same as above             
```
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
```
### 160. Intersection of Two Linked Lists
A slow approach in O(n^2)             
```
ListNode *getIntersectionNode(ListNode *headA, ListNode *headB) {
        ListNode* result;
        ListNode* temp=headB;
        while(headA){
            if(headA==temp){
                result=headA;
                break;
            } 
            else{
                temp=temp->next;
            }
            if(temp==nullptr){
                headA=headA->next;
                temp=headB;
            }
        }
        return result;
    }
```             
### 168. Excel Sheet Column Title             
```
string convertToTitle(int columnNumber) {
        string res="";
        int v;
        while(columnNumber>0){
            v=columnNumber%26;
            if(v==0){
             v=26;  
            }
            res=(char)(v+64)+res; 
            columnNumber-=v;
            columnNumber/=26;
        }
        return res;
    }             
```

### Majorith Elements
The trick here is count-- when it is not the number, also never let the count become a negative number.             
```
int majorityElement(vector<int>& nums) {
        int current=-1;
        int count=0;
        for(auto i:nums){
            if(count==0)
                current=i;
            if(current==i)
                count++;
            else
                count--;
        }
        
        return current;
    }
```
### 344. Reverse String
two pointer way             
```
void reverseString(vector<char>& s) {
        int start=0;
        int end=s.size()-1;
        while(start<=end){
            char temp=s[end];
            s[end]=s[start];
            s[start]=temp;
            start++;
            end--;
        }
    }
```
Onion ways recursion, faster than a single loop
```
void ans(vector<char>& s, int left, int right){
        if(left < right){
            swap(s[left],s[right]);
            ans(s,left+1,right-1);
        }
}
void reverseString(vector<char>& s) {
        ans(s,0,s.size()-1);
}             
```

### 289. Game of Life
not in place and not padding method but at least guarantee in time.         
```
int single_cell_case(vector<vector<int>>& board,int x, int y){ //use for single cell statistic, return the value of its total neighbors
        int rol=board.size()-1;
        int column=board[0].size()-1;
        if(x==0){
            if(y==0){
                return board[x][y+1]+board[x+1][y]+board[x+1][y+1];
            }else if(y==column){
                return board[x][y-1]+board[x+1][y]+board[x+1][y-1];
            }else{
                return board[x][y+1]+board[x][y-1]+board[x+1][y-1]+board[x+1][y]+board[x+1][y+1];
            }
        }else if(x==rol){
            if(y==0){
                return board[x-1][y]+board[x-1][y+1]+board[x][y+1];
            }else if(y==column){
                return board[x][y-1]+board[x-1][y-1]+board[x-1][y];
            }else{
                return board[x][y-1]+board[x-1][y-1]+board[x-1][y]+board[x-1][y+1]+board[x][y+1];
            }
        }else{
            if(y==0){
                return board[x-1][y]+board[x+1][y]+board[x-1][y+1]+board[x][y+1]+board[x+1][y+1];
            }else if(y==column){
                return board[x-1][y]+board[x+1][y]+board[x-1][y-1]+board[x][y-1]+board[x+1][y-1];
            }else{
                return board[x-1][y-1]+board[x-1][y]+board[x-1][y+1]+board[x+1][y]+board[x][y+1]+board[x+1][y+1]+board[x][y-1]+board[x+1][y-1];
            }
        }
    }
    
    void gameOfLife(vector<vector<int>>& board) {
        int rol=board.size()-1;
        int column=board[0].size()-1;
        
        if(rol==0 and column==0){ //special case
            if(board[0][0]==1)
                board[0][0]=0;
        }
        else if(rol==0){
            for(int y=0;y<=column;y++){ //special case
                board[0][y]=0;
            }
        }else if(column==0){
            for(int x=0;x<=rol;x++){ //special case
                board[x][0]=0;
            }
        }    
        else{
            vector<vector<int>> result;
            for(int x=0;x<=rol;x++){
                vector<int> new_line;
                    for(int y=0;y<=column;y++){
                        int scan=single_cell_case(board,x,y);
                        if(board[x][y]==1 and scan<2)
                            new_line.push_back(0);  
                        else if(board[x][y]==1 and (scan==2 or scan==3))
                            new_line.push_back(1);
                        else if(board[x][y]==1 and scan>3)
                            new_line.push_back(0);
                        else if(board[x][y]==0 and scan==3)
                            new_line.push_back(1);
                        else
                            new_line.push_back(0);
                    }
                result.push_back(new_line);
            }
            board=result;
        }    
    }
```
Maximum solution, it is amazing
```
void gameOfLife(vector<vector<int>>& board) {
        int x[4] = {1, -1, 0, 1}, y[4] = {0, 1, 1, 1};
        for (int i=0; i<board.size(); i++) {
            for (int j=0; j<board[0].size(); j++) {
                int sum = board[i][j];
                for (int k=0; k<4; k++) if (i+y[k]<board.size() && j+x[k]<board[0].size() && j+x[k]>=0) {
                        sum += 10 * (board[i+y[k]][j+x[k]]%10);
                        board[i+y[k]][j+x[k]] += 10*(board[i][j]%10);
                }
                if (sum==30 || sum==21 || sum == 31) board[i][j] = 1;
                else board[i][j] = 0;
            }
        }
    }
```

### 495. Teemo Attacking
A memory to record the last hit for counting.
```
int findPoisonedDuration(vector<int>& timeSeries, int duration) {
        int sum=duration;
        
        if(timeSeries.size()==1)
            return sum;
        
        int memory=timeSeries[0];
        for(int i=1;i<timeSeries.size();i++){
            if((memory+duration)>timeSeries[i]){
                sum+=timeSeries[i]-timeSeries[i-1];
                memory=timeSeries[i];
            }else{
                sum+=duration;
                memory=timeSeries[i];
            }
        }
        
        return sum;
    }
```

### 217. Contains Duplicate
a brute force sliding window solution, optimum solution is using a std::set to figure whether set and vector size is equal.
```
bool containsDuplicate(vector<int>& nums) {
        if(nums.size()==1)
            return false;
        int head=0;       
        while(head<nums.size()){
            for(int j=head+1;j<nums.size();j++){
                if(nums[head]==nums[j])
                    return true;
            }
            
            head++;
        } 
        return false;
    }
```

### 219. Contains Duplicate II
almost same sliding windows as above, optimum solution is hashmap.
```
bool containsNearbyDuplicate(vector<int>& nums, int k) {
        if(nums.size()==1)
            return false;
        int head=0;
                        
        while(head<nums.size()){
            for(int j=head+1;j<nums.size();j++){
                if((j-head)<=k){
                    if(nums[head]==nums[j])
                        return true;
                }else
                    break;
            }
            
            head++;
        } 
        return false;
    }
```

### 98. Validate Binary Search Tree
using a min and max pointer to illustrate subtree call
```
bool ans(TreeNode* root, TreeNode* Low, TreeNode* High){
        if(root==nullptr)
            return true;
        if((Low!=nullptr && root->val <= Low->val) || (High!=nullptr && root->val>=High->val))
            return false;
        return ans(root->left,Low,root) and ans(root->right,root,High);
    }
    
bool isValidBST(TreeNode* root) {
        return ans(root,nullptr,nullptr);
    }
```

### 226. Invert Binary Tree
recursion method
```
TreeNode* invertTree(TreeNode* root) {
        if(root==nullptr)
            return nullptr;
        
        invertTree(root->left);
        invertTree(root->right);
        
        TreeNode* temp=root->left;
        root->left=root->right;
        root->right=temp;
        
        return root;
    }
```

### 1557. Minimum Number of Vertices to Reach All Nodes
only need to exclude those point which has an ingress edge
```
vector<int> findSmallestSetOfVertices(int n, vector<vector<int>>& edges) {
        unordered_set<int> element; 
        
        for(auto i:edges){
            element.insert(i[1]);
        }
        
        vector<int> result;
        for(int i=0;i<n;i++){
            if(element.find(i)==element.end())
                result.push_back(i);
        }
        
        return result;
    }
```

### 236. Lowest Common Ancestor of a Binary Tree
recursive call to make sure check, left, right at least have 2 TRUE and that is lowest node.
```
class Solution {
public:
    TreeNode* Result;
    TreeNode* p;
    TreeNode* q;
    bool recurse_tree(TreeNode* current){
        if(current==nullptr)
            return false;
        
        bool left_v=recurse_tree(current->left);
        bool right_v=recurse_tree(current->right);
        bool check= (current==p) or (current==q);
        
        if((int)check+(int)left_v+(int)right_v >=2)
            Result=current;
        return check or left_v or right_v;
    }
    TreeNode* lowestCommonAncestor(TreeNode* root, TreeNode* p1, TreeNode* q2) {
        p=p1;
        q=q2;
        recurse_tree(root);
        return Result;
    }
};
```

### 547. Number of Provinces
Breath FS, queue+visited array+adjacunt array.
```
int findCircleNum(vector<vector<int>>& isConnected) {
        int n=isConnected.size();
        vector<int> visit(n,0);
        vector<int> adj[n];
        for(int i=0;i<n;i++)
            for(int j=0;j<n;j++)
                if(isConnected[i][j]==1)
                    adj[i].push_back(j);
        int ans=0;
        queue<int> q;
        for(int x=0;x<n;x++){
            if(visit[x]==0){
                ans++;
                q.push(x);
                visit[x]=1;
                while(!q.empty()){
                    int node=q.front();
                    q.pop();
                    for(auto it:adj[node]){
                        if(!visit[it]){
                            visit[it]=1;
                            q.push(it);
                        }    
                    }
                }
            }     
        }
        return ans;
    }
```

### 199. Binary Tree Right Side View
```
BFS and return the last node of one loop
vector<int> rightSideView(TreeNode* root) {
        vector<int> result;
        queue<TreeNode*> q;
        
        if(root==nullptr)
            return result;
        
        q.push(root);
        while(!q.empty()){
            int n=q.size();
            for(int i=0;i<n;i++){
                TreeNode* temp=q.front();
                q.pop();
                if(temp->left)
                    q.push(temp->left);
                if(temp->right)
                    q.push(temp->right);
                
                if(i==n-1)
                    result.push_back(temp->val);
            }
        }
        return result;
    }
``` 
 
### 200. Number of Islands
A very decent way to cover area, traverse and if there is an area then replace 1 with 0 and cover its 4-direction neighbors.
``` 
void dfs(vector<vector<char>>& grid, int row, int column){
        int row_limit=grid.size();
        int column_limit=grid[0].size();
        
        grid[row][column]='0';
        
        //go up
        if(row>=1 && grid[row-1][column]=='1')
            dfs(grid,row-1,column);
        //go down
        if(row<(row_limit-1) && grid[row+1][column]=='1')
            dfs(grid,row+1,column);
        //go left
        if(column>=1 && grid[row][column-1]=='1')
            dfs(grid,row,column-1);
        //go right
        if(column<(column_limit-1) && grid[row][column+1]=='1')
            dfs(grid,row,column+1);
    }
    
    int numIslands(vector<vector<char>>& grid) {
        int row=grid.size();
        int column=grid[0].size();
        
        if(row==0)
            return 0;
        
        int count=0;
        
        for(int i=0;i<row;i++){
            for(int j=0;j<column;j++){
                if(grid[i][j]=='1'){
                    count++;
                    dfs(grid,i,j);
                }
            }
        }
        
        return count;
    }
``` 

### 392. Is Subsequence
use Two pointer method to scan the whole string
```
bool isSubsequence(string s, string t) {
        if(s.size()>t.size())
            return false;
        int j=0;
        for(int i=0;i<s.size();i++){
            while(s[i]!=t[j] and j<t.size()){
                j++;
            }
            if(s[i]==t[j])
                j++;
            else if(j==t.size())
                return false;
        }
        return true;
    }
```

### 62. Unique Paths
DP approach, remember to initialize the 0 index in both dimensions first
```
int uniquePaths(int m, int n) {
        int dp[m][n];
        dp[0][0]=1;
        for(int j=1;j<n;j++)
            dp[0][j]=1;
        for(int i=1;i<m;i++)
            dp[i][0]=1;
        
        for(int i=1;i<m;i++){
            for(int j=1;j<n;j++){
                dp[i][j]=dp[i-1][j]+dp[i][j-1];
            }
        }
        return dp[m-1][n-1];
    }
```

### 300. Longest Increasing Subsequence
DP approach,create an array of current subsequence count number, the result needs to be the max value of count array
```
int lengthOfLIS(vector<int>& nums) {
        int len=nums.size();
        int count[len];
        
        count[0]=1;
        for(int i=1;i<nums.size();i++){
            int count_max=0;
            for(int j=0;j<i;j++){
                if(nums[i]>nums[j])
                    count_max=max(count[j],count_max);
            }
            count_max++;
            count[i]=count_max;
        }
        
        int result=1;
        for(auto x:count)
            result=max(result,x);
        return result;
    }
```

### 525. Contiguous Array
Hashmap, treat zero as -1 and record the subsequence sum to be zero, then compare to the max len memory.
```
int findMaxLength(vector<int>& nums) {
        int sum=0;
        int len=0;
        unordered_map<int,int> mp; //sum->index
        mp[0]=-1;
        for(int i=0;i<nums.size();i++){
            if(nums[i]==0)
                sum+=-1;
            else
                sum+=1;
            if(mp.find(sum)==mp.end())
                mp[sum]=i; //do not find sum, insert new index
            else{
                int pre_index=mp[sum];
                len=max(len,i-pre_index);
            }
        }
        return  len;
    }
```
brutal force, very stupid O(n^3)
```
int findMaxLength(vector<int>& nums) {
        int max_length=0;
        for(int i=0;i<nums.size();i++){
            for(int j=nums.size();j>i;j--){
                if( (j-i)<max_length)
                    break;
                
                int zero=0;
                int one=0;
                for(int m=i;m<j;m++){
                    if(nums[m]==1)
                        one++;
                    else
                        zero++;
                }
                
                if(one==zero)
                    max_length=max(max_length,j-i);
            }
        }
        return max_length;
    }
```

### 401. Binary Watch
Remember that bitwise operator & will output the bitwise result, 8&8=8, only translate into bool.
```
vector<string> readBinaryWatch(int turnedOn) {
        vector<string> total;
               
        for(int hour=0;hour<=11;hour++){
            for(int minute=0;minute<=59;minute++){ 
                int hour_count=(bool)(hour&8)+(bool)(hour&4)+(bool)(hour&2)+(bool)(hour&1);
                int minute_count=(bool)(minute&32)+(bool)(minute&16)+(bool)(minute&8)+(bool)(minute&4)+(bool)(minute&2)+(bool)(minute&1);
                if((hour_count+minute_count)==turnedOn){
                    string temp=to_string(hour);
                        temp+=":";
                    if(minute>=10)
                        temp+=to_string(minute);
                    else
                        temp+="0"+to_string(minute);
                    total.push_back(temp);
                }
            }
        }
        return total;
            
    }
```

### 78. Subsets
typical backtrack solution, very elegant code, use index to control forward and use for loop to control back step
```
void backtrack(vector<vector<int>> &res,vector<int> &nums,vector<int> cur, int idx){
        res.push_back(cur);
        for(int i=idx; i<nums.size();i++){
            vector<int> c=cur;
            c.push_back(nums[i]);
            backtrack(res,nums,c,i+1);
        }
    }
        
        
    vector<vector<int>> subsets(vector<int>& nums) {
        vector<vector<int>> res;
        vector<int> cur;
        backtrack(res,nums,cur,0);
        
        return res;
    }
```

###  322. Coin Change
```
int coinChange(vector<int>& coins, int amount) {
        vector<int> dp(amount+1,999);
        dp[0]=0;
        
        if(amount==0)
            return 0;
        
        for(auto x:coins)
            if(x<amount)
                dp[x]=1;
        
        for(int i=1;i<=amount;i++){
            for(auto c:coins)
                if((i-c)>=0)
                    dp[i]=min(dp[i],dp[i-c]+1);
        }
                
        if(dp[amount]==999)
            return -1;
        else
            return dp[amount];
    }
```
# TEMPLATE

Syntax highlighted code block
```
code
```
# Header 1
## Header 2
### Header 3

- Bulleted
- List

1. Numbered
2. List

**Bold** and _Italic_ and `Code` text

[Link](url) and ![Image](src)
