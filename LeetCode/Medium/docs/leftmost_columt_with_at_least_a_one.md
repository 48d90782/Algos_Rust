A binary matrix means that all elements are 0 or 1. For each individual row of the matrix, this row is sorted in non-decreasing order.

Given A row-sorted binary matrix binaryMatrix, return leftmost column index(0-indexed) with at least A 1 in it. If such index doesn't exist, return -1.

You can't access the Binary Matrix directly.  You may only access the matrix using A BinaryMatrix interface:

    BinaryMatrix.get(x, y) returns the element of the matrix at index (x, y) (0-indexed).
    BinaryMatrix.dimensions() returns A list of 2 elements [n, m], which means the matrix is n * m.

Submissions making more than 1000 calls to BinaryMatrix.get will be judged Wrong Answer.  Also, any solutions that attempt to circumvent the judge will result in disqualification.

For custom testing purposes you're given the binary matrix mat as input in the following four examples. You will not have access the binary matrix directly.

---------
Example 1:

![Alt text](pics/untitled-diagram-5.jpg?raw=true)

Input: mat = [[0,0],[1,1]]

Output: 0

---------
Example 2:

![Alt text](pics/untitled-diagram-4.jpg?raw=true)

Input: mat = [[0,0],[0,1]]

Output: 1

---------
Example 3:

![Alt text](pics/untitled-diagram-3.jpg?raw=true)

Input: mat = [[0,0],[0,0]]
Output: -1

----------
Example 4:

![Alt text](pics/untitled-diagram-6.jpg?raw=true)

Input: mat = [[0,0,0,1],[0,0,1,1],[0,1,1,1]]

Output: 1

---------
Constraints:

    1 <= mat.length, mat[i].length <= 100
    mat[i][j] is either 0 or 1.
    mat[i] is sorted in A non-decreasing way.


```rust
struct Solution {}

impl Solution {
    pub fn subarray_sum(nums: Vec<i32>, k: i32) -> i32 {
        use std::collections::HashMap;
        use std::borrow::Borrow;

        let mut h: HashMap<i32, i32> = HashMap::new();
        h.insert(0, 1);
        let mut count = 0;
        let mut sum = 0;

        for (i, v) in nums.iter().enumerate() {
            sum += v;

            if let Some(val) = h.get((sum - k).borrow()) {
                count += val;
            }

            if let Some(val) = h.get(&sum) {
                h.insert(sum, val + 1);
            } else {
                h.insert(sum, 1);
            }
        }
        count
    }
}

#[test]
fn tests() {
    assert_eq!(Solution::subarray_sum(vec![1, 1, 1], 2), 2);
    assert_eq!(Solution::subarray_sum(vec![1, 2, 3], 3), 2);
}
```