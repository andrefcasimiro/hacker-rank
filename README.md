
# Sock Merchant

## Description:
John works at a clothing store. He has a large pile of socks that he must pair by color for sale. Given an array of integers representing the color of each sock, determine how many pairs of socks with matching colors there are.

For example, there are n=7 socks with colors ar = [1, 2, 1, 2, 1, 3, 2]. There is one pair of color  and one of color . There are three odd socks left, one of each color. The number of pairs is 2.

## Function Description:

Complete the sockMerchant function in the editor below. It must return an integer representing the number of matching pairs of socks that are available.

sockMerchant has the following parameter(s):

- n: the number of socks in the pile
- ar: the colors of each sock

## Input Format

The first line contains an integer n, the number of socks represented in ar.
The second line contains n space-separated integers describing the colors ar[i] of the socks in the pile.

## Constraints

1 <= n <= 100
1 <= ar[i] <= 100 where 0 <= i < n

## Output format

Return the total number of matching pairs of socks that John can sell.


### Proposed Solution:
```
function sockMerchant(n, ar) {
  if (!n) {
    n = ar.length;
  }

  let possiblePairs = 0;
  let visited = [];

  for (let i = 0; i < n; i++) {
    let count = 0;

    if (visited.includes(ar[i])) {
      continue;
    } else {
      visited.push(ar[i]);
    }

    for (let j = i; j < ar.length; j++) {
      if (ar[i] === ar[j]) {
        count++;

        if (count % 2 === 0) {
          possiblePairs++;
        }
      }
    }
  }

  return possiblePairs
}
```
