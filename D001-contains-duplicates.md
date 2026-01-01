## # question

[contains duplicate](https://leetcode.com/problems/contains-duplicate/)

## # thought process

- loop through values
- save intergers as keys in a map with a boolean value
- check map value on every loop
- if value is true, contains duplicate, exit loop & return
- this avoids nested loops [O(n²)]

## # concept

hashmaps?

## # implementation

### go

```go
func containsDuplicate(nums []int) bool {
	lookupStore := make(map[int]bool)

	for _, n := range nums {
		seen := lookupStore[n]

		if seen {
			return true
		}

		lookupStore[n] = true
	}

	return false
}
```

<img width="986" height="198" alt="Screenshot 2026-01-01 at 22 11 59" src="https://github.com/user-attachments/assets/1888f697-f1c0-48b0-89ef-48af16330bd6" />




### typescript
```typescript
function containsDuplicate(nums: number[]): boolean {
    const lookupStore: Map<number, boolean> = new Map()

    for (let i = 0; i < nums.length; i++) {
        if (lookupStore.get(nums[i])) {
            return true
        }

        lookupStore.set(nums[i], true)
    }

    return false
};
```

<img width="986" height="198" alt="Screenshot 2026-01-01 at 22 11 52" src="https://github.com/user-attachments/assets/39c0a71c-6393-450b-985f-95bbbf7c72ee" />


## # complexity

- **time complexity:** O(n)
- **space complexity:** O(n)
