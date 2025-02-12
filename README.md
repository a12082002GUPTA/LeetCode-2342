# LeetCode-2342

# C++

class Solution {
public:
    int maximumSum(vector<int>& nums) {
        map<int,vector<int>>mp;
        sort(nums.begin(),nums.end());
        for(int i=0;i<nums.size();i++)
        {
            int sum=0,dup=nums[i];
            while(dup)
            {
                sum+=(dup%10);
                dup/=10;
            }
            mp[sum].push_back(nums[i]);
        }
        int ans=-1;
        for(auto i:mp)
        {
            if(i.second.size()>1)
            {
                int n=i.second.size();
                int sum=i.second[n-1]+i.second[n-2];
                ans=max(ans,sum);
            }
        }
        return ans;
    }
};

# Python

from collections import defaultdict

class Solution:
    def maximumSum(self, nums):
        num_map = defaultdict(list)
        nums.sort()

        for num in nums:
            digit_sum = sum(int(digit) for digit in str(num))
            num_map[digit_sum].append(num)

        ans = -1
        for values in num_map.values():
            if len(values) > 1:
                ans = max(ans, values[-1] + values[-2])

        return ans

# Example usage:
solution = Solution()
nums = [51, 71, 17, 42]
print(solution.maximumSum(nums))  # Output: 93

# Java

import java.util.*;

class Solution {
    public int maximumSum(int[] nums) {
        Map<Integer, List<Integer>> numMap = new HashMap<>();
        Arrays.sort(nums);
        
        for (int num : nums) {
            int digitSum = getDigitSum(num);
            numMap.putIfAbsent(digitSum, new ArrayList<>());
            numMap.get(digitSum).add(num);
        }
        
        int ans = -1;
        for (List<Integer> values : numMap.values()) {
            if (values.size() > 1) {
                int n = values.size();
                ans = Math.max(ans, values.get(n - 1) + values.get(n - 2));
            }
        }
        
        return ans;
    }
    
    private int getDigitSum(int num) {
        int sum = 0;
        while (num > 0) {
            sum += num % 10;
            num /= 10;
        }
        return sum;
    }
    
    public static void main(String[] args) {
        Solution solution = new Solution();
        int[] nums = {51, 71, 17, 42};
        System.out.println(solution.maximumSum(nums)); // Output: 93
    }
}
