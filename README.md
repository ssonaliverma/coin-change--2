# coin-change--2

int  solve(int index,int tar,vector<int>&c,vector<vector<int>>&dp)
    {
        if(tar==0) return 1;
        if(index<0)return 0;//not possible way
        
        if(dp[index][tar]!=-1)
        {
            return dp[index][tar];
        }
        int way=0;
        for(int coin =0; coin<=tar; coin+=c[index])
        {
            way+=solve(index-1, tar-coin, c, dp);
        }

        return dp[index][tar]=way;
    }


     int  solve2(int index,int tar,vector<int>&c,vector<vector<int>>&dp)
    {
        if(tar==0) return 1;
        if(index<0)return 0;//not possible way
        
        if(dp[index][tar]!=-1)
        {
            return dp[index][tar];
        }
        
        long long int take=0;
        if(tar-c[index]>=0)
        {
            take=solve2(index,tar-c[index],c,dp);
        }
        
        long long int notTake=solve2(index-1, tar, c , dp);
        
        return dp[index][tar]=take+notTake;
    }


    

    int change(int amount, vector<int>& coins) {
      
      
        vector<vector<int>>dp(coins.size()+2,vector<int>(amount+1,-1));
        return solve2(coins.size()-1,amount,coins,dp);
    }
