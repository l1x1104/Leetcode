[Bold Words in String] (https://leetcode.com/problems/bold-words-in-string/description/)

这道题让我们把字符串在字典中加粗. <br>
思路是建一个和字典s等长的布尔型数组，如果该字符在单词里面就为true，最后我们就可以根据数组的真假值来添加标签了. <br>
我们遍历字符串中的每一个字符，把遍历到的每一个单词当作起始位置，我们匹配一遍字典中的所有单词，如果能匹配上，我们就用i + len来更新end，len是当前单词的长度，end表示字典中的单词在字符串s中结束的位置，那么如果i小于end，bold[i]就要赋值为true了


