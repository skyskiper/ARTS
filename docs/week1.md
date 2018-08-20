##Algorithm 

###[Regular Expression Matching](https://leetcode.com/problems/regular-expression-matching/description/)
Given an input string (s) and a pattern (p), implement regular expression matching with support for '.' and '*'.

- '.' Matches any single character.
- '*' Matches zero or more of the preceding element.

The matching should cover the entire input string (not partial).

Note:

- s could be empty and contains only lowercase letters a-z.
- p could be empty and contains only lowercase letters a-z, and characters like . or *.

Code:

    class Solution {
        public boolean isMatch(String text, String pattern) {
            boolean[][] dp = new boolean[text.length() + 1][pattern.length() + 1];

            //注意 dp[text.length()][x]的初始化不是简单的设为true或者false
            dp[text.length()][pattern.length()] = true;
            for (int i = text.length(); i >= 0; i--) {
                for (int j = pattern.length() - 1; j >= 0; j--) {
                    boolean equals = i < text.length() && (text.charAt(i) == pattern.charAt(j) || pattern.charAt(j) == '.');
                    if (j < pattern.length() - 1 && pattern.charAt(j + 1) == '*') {
                        dp[i][j] = dp[i][j + 2] || (equals && dp[i + 1][j]);
                    } else {
                        dp[i][j] = equals && dp[i + 1][j + 1];
                    }
                }
            }
            return dp[0][0];
        }
    }
     
##Review
DNS的历史和域名分层，DNS工作原理

<https://medium.com/zkcapital/handshake-ens-and-decentralized-naming-services-explained-2e69a1ca1313/>

##Tip

工作中公司代码是gitlab来托管代码，而个人代码则倾向于托管在github上。个人邮箱与公司邮箱又不相同，因此生成的ssh key不相同。所以如何管理不同的私钥呢？

生成 ssh 公/私钥对

    # 工作用
    ssh-keygen -t rsa -C "工作邮箱"
    # 个人用
    ssh-keygen -t rsa -f ~/.ssh/id_rsa_github -C "个人邮箱"
    
配置文件 ~/.ssh/config

    Host gitlab.company.com
    User git
    IdentityFile ~/.ssh/id_rsa
    
    Host github.com
    User git
    IdentityFile ~/.ssh/id_rsa_github

##Share
hash算法

<https://medium.com/zkcapital/the-state-of-hashing-algorithms-the-why-the-how-and-the-future-b21d5c0440de/>

