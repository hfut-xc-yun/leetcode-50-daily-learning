#原题:[https://leetcode-cn.com/problems/string-to-integer-atoi](https://leetcode-cn.com/problems/string-to-integer-atoi)

##总体思路：
1.从第一个+，-，数字中向后提取是数字的连续字符串；
2.对已提取的连续字符串逐字符做数字转换；
3.注意边界值处理，如果超出范围返回INT32上下界，对于C++，用long型作为暂存数字，可能输入超出INT上下界；

##代码(C++)
	class Solution {
	public:
    int myAtoi(string s) {
        int i = 0;
        long ret = 0;
        string num;
        int flag = 1;
        while(!s.empty()){
            if(s[0]!=' ') break;
            else s.erase(0,1);
        }
        if(s[0]=='+'){
            flag = 1;
            s.erase(0,1);
        }
        else if(s[0]=='-'){
            flag = -1;
            s.erase(0,1);
        }
        else if(s[0]<'0'||s[0]>'9'){
            return 0;
        }

        while(!s.empty()){
            if(s[0]>='0'&& s[0]<='9'){
                num.push_back(s[0]);
                s.erase(0,1);
            }
            else break;
        }

        for(auto c:num){
            if(ret-1>INT_MAX) break;
            else ret = ret*10 + int(c-'0');
        }
        ret=flag*ret;
        if(ret>INT_MAX)return INT_MAX;
        if(ret<INT_MIN)return INT_MIN;

        return ret;
    }
	};

#效率
执行用时：0ms，击败100%

内存消耗：7.3MB,击败48%