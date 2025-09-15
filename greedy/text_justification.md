# LeetCode 68: Text Justification (Hard)
### Problem Description:

Given an array of strings words and a width maxWidth, format the text such that each line has exactly maxWidth characters and is fully (left and right) justified.

You should pack your words in a greedy approach; that is, pack as many words as you can in each line. Pad extra spaces ' ' when necessary so that each line has exactly maxWidth characters.

Extra spaces between words should be distributed as evenly as possible. If the number of spaces on a line does not divide evenly between words, the empty slots on the left will be assigned more spaces than the slots on the right.

For the last line of text, it should be left-justified, and no extra space is inserted between words.

### Approach:

**Time complexity: O(n * maxWidth)**

**Space complexity: O(n * maxWidth)**

This is a very annoying problem solely because of the amount of edge cases we need to account for, but ultimately it isn't as complex
as some other problems that require multiple data structures. We're just iterating and managing strings.

We'll keep an array curLine to represent the current line we're working on. Iterating through words, we will greedily add as many words as 
we can to the line, only stopping once the next word won't be able to fit (this includes spaces). Once this happens, we know our current
line is ready to be processed. We need to add spaces between the words, so we'll find the total empty space within the line, then divide it
by the length of our curList - 1 to get the length of each space. We also use the modulo operator to keep track of our remainder that we 
will add on later. 

We have to be careful of edge cases, specifically when our line only contains 1 word as 1) it could cause 0 division, 
but also 2) lines with only 1 word need left alignment. A somewhat elegant solution to this is using max() with 1 inside as a buffer so
that 0 divison can't occur, and our space appending loop is guaranteed to occur at least once with every line.

Then, we simply add on the appropriate amount of spaces to each word in our curLine (and an extra if remainder is a positive value), then 
join them together. We have our line and can append it. We do this until our pointer reaches the length of words. 

However, our code doesn't actually do anything with our final line once our while loop ends, so we need to manually add on the last line.
We'll join the words in this final line with a space and calculate the amount of spaces to add on at the end, and we're done!





``` python
class Solution(object):
    def fullJustify(self, words, maxWidth):
        """
        :type words: List[str]
        :type maxWidth: int
        :rtype: List[str]
        """
        ans = []
        curLine, length = [], 0
        i = 0

        while i < len(words):
            if length + len(curLine) + len(words[i]) > maxWidth:
                totalSpace = maxWidth - length
                perSpace = totalSpace // max(1, (len(curLine) - 1))
                remainder = totalSpace % max(1, (len(curLine) - 1))

                for x in range(max(1, len(curLine) - 1)):
                    curLine[x] += " " * perSpace
                    if remainder:
                        curLine[x] += " "
                        remainder -= 1
                ans.append("".join(curLine))
                curLine, length = [], 0

            curLine.append(words[i])
            length += len(words[i])
            i += 1
        
        lastLine = " ".join(curLine)
        extraSpaces = maxWidth - len(lastLine)
        ans.append(lastLine + " " * extraSpaces)
        return ans

```
