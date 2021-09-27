# Leetcode notes
Reach me with ncdenaozi@outlook.com

## 7. Reverse Integer
use brutal force to solve this method, note that there already exists a macro called INT_MAX and INT_MIN in cpp std library, or can use (1<<31)-1 as max count.
**really bad idea not to use a stack instead of a vector :<**
`int reverse(int x) {
        
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
    }`
    
## 9. Palindrome Number
use simple vector not stack. I thought vector may be easier to control with head&tail pointer because it is quite difficult to remember the number poped out of stack, probably need another memory list?
Speed is quite slow, optimal solution is that we only need to reverse half of the number, kind of tricky one.
`bool isPalindrome(int x) {
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
    }`
    
## 13. Roman to Integer
A hashmap<char,int>. Note that normal ROMAN NUMBER is written in large-to-small but things like IV is actually small to large, so have a memory to locate the last ROMAN digit.
**Pity that leetcode need premium to unlock the standard solution.**
` int romanToInt(string s) {
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
}; `


## 14. Longest Common Prefix
Brute force with a decoder-like program, just runs the whole comparison char by char.
standard solution is using **divide and conquer**, I like the idea but the implementation could be fussy.
` string longestCommonPrefix(vector<string>& strs) {
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
}; `
    
  


## 20. Valid Parentheses
I fail for the first time because I am thinking how can I deal with the right side parenthese in the stack. But then I found out that only left-side parentheses should be pushed into the stack and the right-side is only used as a comparison.
`bool isValid(string s) {`
`        if(s.size()%2==1)
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
}   `

## 26. Remove Duplicates from Sorted Array
Use std::vector.erase(vector.begin()+i) to delete one element from the space. Note that after delete operation, the position and the size both reduce itself so i-- is needed.
Speed is quite slow, standard solution is in JAVA.
`
    int removeDuplicates(vector<int>& nums) {
        for(int i=1;i<nums.size();i++){
            if(nums[i]<=nums[i-1]){
                nums.erase(nums.begin()+i);
                i--;
            }
        }
        return nums.size();
    }
`

## 27. Remove Element
Almost same as problem 26.
`
     int removeElement(vector<int>& nums, int val) {
        for(int i=0;i<nums.size();i++){
            if(nums[i]==val){
                nums.erase(nums.begin()+i);
                i--;
            }
        }
        return nums.size();
    }
`

## 28. implement strStr()
Use std::string.compare(int position, int length, string substring) and traverse the haystack, there is a lot of corner case so add a few conditions.
`
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

`




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
