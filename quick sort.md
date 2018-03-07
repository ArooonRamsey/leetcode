this is the first time to meet a problem that needs quick sort or heap sort to solve.

[最小的K个数](https://www.nowcoder.com/practice/6a296eb82cf844ca8539b57c23e6e9bf?tpId=13&tqId=11182&tPage=2&rp=2&ru=%2Fta%2Fcoding-interviews&qru=%2Fta%2Fcoding-interviews%2Fquestion-ranking)

快排的主要思想是，在一个数组中，用其中的一个数来作为划分依据：

小于这个数的，放在左边；大于这个数的，放在右边。

如果要实现的话，则需要通过两个遍历变量来实现，变量**first**和**index**，first是用来遍历的，遍历到小于标准数的时候，和index交换，index同时+1；
分析这个逻辑，如果遇到这个数比标准数大，那么index一直指着这个数，一直到有first遍历到一个小数字，和这个index交换；只要遇到一个较小的数就会被提到前面。
始终不会出现已经遍历过的数字中小于标准数的在大于标准数的右侧。

在最小数问题中，这个思想可以借鉴。

here is the solution of mine, pay attention that function **partition** can be used in many scene.
``` c++
class Solution {
public:
    void swap(int& lhs, int& rhs) {
        int tmp = lhs;
        lhs = rhs;
        rhs = tmp;
    }
    
    int partition(vector<int>& input , int first , int last) {
        if(first == last) return first;
        int index;
        for(index = first ; first != last ; first++){
            if(input[first] < input[last]) {
                swap(input[first],input[index++]);
            }
        }
        swap(input[index], input[last]);
        return index;
    }
    
    vector<int> GetLeastNumbers_Solution(vector<int> input, int k) {
        vector<int> iRet;
        if(input.size() < k) return iRet;
        else if(input.size() == k) return input;
        int first = 0;
        int last = input.size() - 1;
        int index = -1;
        while(index != k - 1) {
            index = partition(input , first , last);
            if(index < k - 1) {
                first = index + 1;
            }
            if(index > k - 1) {
                last = index - 1;
            }
        }
        for(index = 0 ; index != k ; index++) {
            iRet.push_back(input[index]);
        }
        return iRet;
    }
};
```
