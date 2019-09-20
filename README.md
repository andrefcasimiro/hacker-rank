# Hacker Ranks Code Challenges

1. [Sock Merchant](#sock-merchant)
2. [Grading Students](#grading-students)
3. [Counting Valleys](#counting-valleys)
4. [Jumping On The Clouds](#jumping-on-the-clouds)

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

# Grading Students

## Description:
HackerLand University has the following grading policy:

- Every student receives a grade in the inclusive range from 0 to 100.
- Any grade less than 40 is a failing grade.

Sam is a professor at the university and likes to round each student's grade according to these rules:

- If the difference between the grade and the next multiple of 5 is less than 3, round  up to the next multiple of 5;
- If the value of grade is less than 38, no rounding occurs as the result will still be a failing grade.

For example, grade 84  will be rounded to 85 but grade = 29 will not be rounded because the rounding would result in a
number that is less than 40.

Given the initial value of grade for each of Sam's n students, write code to automate the rounding process.

## Function Description:

Complete the function gradingStudents in the editor below. It should return an integer array consisting of rounded grades.

gradingStudents has the following parameter(s):

- grades: an array of integers representing grades before rounding

## Input Format

The first line contains a single integer, n, the number of students.

Each line i of the n subsequent lines contains a single integer, grades[i], denoting student i's grade.

## Constraints

1 <= n <= 60
0 <= grades[i] <= 100

## Output format

For each grades[i], print the rounded grade on a new line.

### Proposed Solution:
```
function gradingStudents(grades) {
  return grades.map(grade => {
    if (grade < 38) {
      return grade
    }

    let nextMultipleOf5;
    for (let i = grade; i <= 100; i++) {

      if (i % 5 === 0) {
        nextMultipleOf5 = i;
        break;
      }
    }

    return nextMultipleOf5 - grade < 3
      ? nextMultipleOf5
      : grade;
  })
}
```

# Counting Valleys

## Description:
Gary is an avid hiker. He tracks his hikes meticulously, paying close attention to small details like topography. During his last hike he took exactly n steps. For every step he took, he noted if it was an uphill, U , or a downhill, D step. Gary's hikes start and end at sea level and each step up or down represents a 1 unit change in altitude. We define the following terms:

- A mountain is a sequence of consecutive steps above sea level, starting with a step up from sea level and ending with a step down to sea level.
- A valley is a sequence of consecutive steps below sea level, starting with a step down from sea level and ending with a step up to sea level.

Given Gary's sequence of up and down steps during his last hike, find and print the number of valleys he walked through.

For example, if Gary's path is s = [DDUUUUDD], he first enters a valley 2 units deep. Then he climbs out an up onto a mountain 2 units high. Finally, he returns to sea level and ends his hike.

## Function Description:

Complete the countingValleys function in the editor below. It must return an integer that denotes the number of valleys Gary traversed.

countingValleys has the following parameter(s):

n: the number of steps Gary takes
s: a string describing his path

## Input Format

The first line contains an integer n, the number of steps in Gary's hike.

The second line contains a single string s, of n characters that describe his path.

## Constraints

2 <= n <= 10^6
s[i] € {UD}

## Output format

Print a single integer that denotes the number of valleys Gary walked through during his hike.

### Proposed Solution:
```
function countingValleys(n, s) {
    if (!n) {
      var n = s.length;
    }

    const graph = (s.split('')).map(step => step === 'U' ? 1 : -1);

    let currentDepth = 0;
    let enterValley = 0;

    for (let i = 0; i < n; i++) {
        if (currentDepth === 0 && currentDepth + graph[i] < 0) {
           enterValley++;
        }

        currentDepth += graph[i];
    }

  return enterValley;
}
```

# Jumping On The Clouds

## Description:
Emma is playing a new mobile game that starts with consecutively numbered clouds. Some of the clouds are thunderheads and others are cumulus. She can jump on any cumulus cloud having a number that is equal to the number of the current cloud plus 1 or 2. She must avoid the thunderheads. Determine the minimum number of jumps it will take Emma to jump from her starting postion to the last cloud. It is always possible to win the game.

For each game, Emma will get an array of clouds numbered 0 if they are safe or 1 if they must be avoided. For example,
c = [0, 1, 0, 0, 0, 1, 0]  indexed from 0 ... 6 The number on each cloud is its index in the list so she must avoid the clouds at indexes 1 and 5. She could follow the following two paths: 0 -> 2 -> 4 -> 6 or 0 -> 2 -> 3 -> 4 -> 6. The first path takes 3 jumps while the second takes 4.

## Function Description:

Complete the jumpingOnClouds function in the editor below. It should return the minimum number of jumps required, as an integer.

jumpingOnClouds has the following parameter(s):

- c: an array of binary integers

## Input Format

The first line contains an integer n, the total number of clouds. The second line contains n space-separated binary integers describing clouds c[i] where 0 <= i < n.

## Constraints

2 <= n <= 100
c[i] € {0, 1}
c[0] = c[n - 1] = 0

## Output format

Print the minimum number of jumps needed to win the game.

### Proposed Solution:
```
function jumpingOnClouds(c) {

  let numberOfJumps = 0;

  for (let i = 0; i < c.length; i++) {
    if (c[i + 2] === 0) {
      numberOfJumps++;
      i = i + 1;
    } else if (c[i + 1] === 0) {
      numberOfJumps++;
    }
  }

  return numberOfJumps;
}
```
