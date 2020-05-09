设计一个函数把两个数字相加。不得使用 + 或者其他算术运算符。

示例:

输入: a = 1, b = 1
输出: 2

 

提示：

    a, b 均可能是负数或 0
    结果不会溢出 32 位整数

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/add-without-plus-lcci
class Solution {
public:
    int add(int a, int b) {
        return a-(-1*b);
    }
};

异或运算实现加法
//不用+-*/的加法
class Solution {
public:
    static int add(int a,int b)
    {
        int sum = 0, c = 0;//和，进位
        while (b != 0)
        {
            sum = a ^ b;//异或运算表示二进制的非进位和
            c = (a & b) << 1;//与运算左移一位补0表示二进制的进位和;注意<<的优先级高于&，需要括号
            //更新a，b为非进位和，进位和
            a = sum;
            b = c;    //进位为0时结束运算
            
        }
 
        return a;
    }
};



给你两个 非空 链表来代表两个非负整数。数字最高位位于链表开始位置。它们的每个节点只存储一位数字。将这两数相加会返回一个新的链表。

你可以假设除了数字 0 之外，这两个数字都不会以零开头。

 

进阶：

如果输入链表不能修改该如何处理？换句话说，你不能对列表中的节点进行翻转。

 

示例：

输入：(7 -> 2 -> 4 -> 3) + (5 -> 6 -> 4)
输出：7 -> 8 -> 0 -> 7

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/add-two-numbers-ii
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode(int x) : val(x), next(NULL) {}
 * };
 */
class Solution {
public:
    ListNode* addTwoNumbers(ListNode* l1, ListNode* l2) {
		stack<int>p1,p2;
		while(l1!=NULL)
		{
			p1.push(l1->val);
			l1=l1->next;
		}
		while(l2!=NULL)
		{
			p2.push(l2->val);
			l2=l2->next;
		}
		ListNode* head=nullptr;
		int carry=0;
		while(!p1.empty()||!p2.empty()||carry!=0)
		{
			int a=0,b=0;
			if(!p1.empty()){
				a=p1.top();
				p1.pop();
			}
			if(!p2.empty()){
				b=p2.top();
				p2.pop();
			}
			int now=a+b+carry;
			carry=now/10;
			now=now%10;
			ListNode* temp=new ListNode(0);
			//头插法
			temp->val=now;
			temp->next=head;
			head=temp;
		}
		return head;
    }
};
