输入一个整型数组，数组里有正数也有负数。数组中的一个或连续多个整数组成一个子数组。求所有子数组的和的最大值。

要求时间复杂度为O(n)。

 

示例1:

输入: nums = [-2,1,-3,4,-1,2,1,-5,4]
输出: 6
解释: 连续子数组 [4,-1,2,1] 的和最大，为 6。

 

提示：

    1 <= arr.length <= 10^5
    -100 <= arr[i] <= 100

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/lian-xu-zi-shu-zu-de-zui-da-he-lcof

---------------模拟-------------
class Solution {
public:
    int maxSubArray(vector<int>& nums) {
		int ans=-9999999;
		int temp=0;
		int len=nums.size();
		for(int i=0;i<len;i++)
		{
			temp=temp+nums[i];
			if(temp<0){
				temp=0;
			}
			else if(temp>=ans){
				ans=temp;
			}
		}
		if(ans==-9999999)
		{
			for(int i=0;i<len;i++){
				ans=max(nums[i],ans);
			}
		}
        return ans;
    }
};

输入一个字符串，打印出该字符串中字符的所有排列。

 

你可以以任意顺序返回这个字符串数组，但里面不能有重复元素。

 

示例:

输入：s = "abc"
输出：["abc","acb","bac","bca","cab","cba"]

 

限制：

1 <= s 的长度 <= 8
class Solution {
public:
	char a[20];
	vector<string>p;
    vector<string> permutation(string s) {
		int len=s.length();
		for(int i=0;i<len;i++){
			a[i]=s[i];
		}
		sort(a,a+len);
		do
		{
			string temp="";
			for(int i=0;i<len;i++){
				temp=temp+a[i];
			}
			p.push_back(temp);
		} while (next_permutation(a,a+len));
		return p;
    }
};

面试题51. 数组中的逆序对

在数组中的两个数字，如果前面一个数字大于后面的数字，则这两个数字组成一个逆序对。输入一个数组，求出这个数组中的逆序对的总数。

 

示例 1:

输入: [7,5,6,4]
输出: 5

 

限制：

0 <= 数组长度 <= 50000
-------------------归并排序的应用---------------
class Solution {
public:
	int ans = 0;
	void merge(int le, int mid, int ri,  vector<int>& a)
	{
		int temp[50005];
		int i = le, j = mid + 1;
		int n = mid, m = ri;
		int k = 0;
		while (i <= n && j <= m)
		{
			if (a[i] <= a[j]) {
				temp[k++] = a[i++];
			}
			else {
				temp[k++] = a[j++];
				ans = ans + mid - i + 1;
			}
		}
		while (i <= n) {
			temp[k++] = a[i++];
		}
		while (j <= m) {
			temp[k++] = a[j++];
		}
		for (int i = 0; i < k; i++) {
			a[le + i] = temp[i];
		}
	}
	void quick_pow(int le, int ri, vector<int>&a)
	{
		if (le >= ri) {
			return;
		}
		int mid = (le + ri) / 2;
		quick_pow(le, mid, a);
		quick_pow(mid + 1, ri, a);
		merge(le, mid, ri, a);
	}
	int reversePairs(vector<int>& nums) {
		int l = 0, r = nums.size() - 1;
		quick_pow(l, r, nums);
		return ans;
	}
};
