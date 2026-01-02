## # question

[valid anagram](https://leetcode.com/problems/valid-anagram/)

## # thought process

-  we basically want to check if all letters in a word is present in another
-  we haver to loop through word A & B to compare values
-  we want to find a way to avoid running nested loops for optimal performance
-  what if we merge them into one array or map that doesn't allow duplicates?

-  loop through one array (doesn't matter which, they're same length)
-  store values as value+count key pairs
-  now we have a single record for every character

-  how do we check if anagram?
-  what if we stored duplicates
-  and then check the length of final map againt length of t - dups & length of s - dups
-  what if we us a balance sheet record
-  then we increment count on appearance in s and decrement on appearance in t
-  all counts must be zero at the end.

## # concept

not sure but i used hashmaps, i'm certain there is a much more defined idea for this kind of problems

## # implementation

### go

```go
func isAnagram(s string, t string) bool {
	// first, if not same length, then it is not an anagram
	if len(s) != len(t) {
		return false
	}

	balanceRecord := make(map[rune]int)
    nonZero := 0 

	for i := 0; i < len(s); i++ {
		sChar, tChar := rune(s[i]), rune(t[i])

        // increment nonZero tracker for s
		if balanceRecord[sChar] == 0 {
			nonZero++
		} 

        // add s character to balance sheet
        balanceRecord[sChar]++

        // check if balance is zero
        // if balance is zero after incrementing
        // it means the previous balance was -1 so we can tell we have a value that doesn't check out
        if balanceRecord[sChar] == 0 {
            nonZero--
        }

		// increment nonZero tracker for t
		if balanceRecord[tChar] == 0 {
			nonZero++
		} 

        // reduce count in balance sheet
        // a is supposed to balance it back to zero if character exists in a
        balanceRecord[tChar]--

        // check if balance is zero
        // if balance is zero after incrementing
        // it means the previous balance was -1 so we can tell we have a value that doesn't check out
        if balanceRecord[tChar] == 0 {
            nonZero--
        }

        // there's a possibility that a count could be less than -1
        // if this happens, then we don't need to do anything since we already recorded the nonZero tracker 
        // already when it was negative the first time
	}

	return nonZero == 0
}
```
<img width="980" height="193" alt="Screenshot 2026-01-02 at 23 30 45" src="https://github.com/user-attachments/assets/75e5f10a-7848-464d-a543-5e81e2aa51c4" />



## # complexity

- **time complexity:** O(n)
- **space complexity:** O(1)

