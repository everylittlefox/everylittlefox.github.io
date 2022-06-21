---
layout: post
title: divide and conquer algorithms
date: 2022-06-10 10:32 +0100
categories: dsa
in_progress: true
---

## merge sort

Merge sort is a divide and conquer sorting algorithm that runs in $O(n\log{n})$ time. Like all sorting algorithms, it takes an array of `n` numbers and returns a sorted array of those `n` numbers.

The concept of how the algorithm is summed up in two observations:

1. it is easier to sort a smaller array than a larger one, and
2. it is fairly easy to form a sorted array of $m+n$ numbers from two sorted arrays of lengths `m` and `n`. (This is done in $O(n)$ time by running through both arrays in parallel as we'll see later.)

The base case of the algorithm stems from the first observation. If the ease of sorting an array increases as its size decreases, then an array with just one element should be the easiest to sort. It is--an array with just one element is already sorted and can be returned as the result of the algorithm.

```javascript
if (arr.length == 1) return arr
```

At the heart of every divide and conquer algorithm is its combine step--how it (correctly) forms the final result from the results of the several recursive calls it made.


```javascript
function mergeSort(arr, extractor = k => k) {
  if (arr.length <= 1) return arr;

  const combine = (left, right) => {
    const leftL = left.length;
    const rightL = right.length;
    const result = Array.from({ length: leftL + rightL });

    let i = 0;
    let j = 0;
    for (let k = 0; k < result.length; k++) {
      if (extractor(left[i]) < extractor(right[j])) {
        result[k] = left[i];
        i++;
      } else {
        result[k] = right[j];
        j++;
      }
    }
    return result;
  };

  const mid = Math.floor(arr.length / 2)
  const left = arr.slice(0, mid)
  const right = arr.slice(mid)

  return combine(mergeSort(left), mergeSort(right))
}
```

```javascript

// Points: {x: 0, y: 0}
function closestPair(px, py) {
  const mid = Math.floor(arr.length / 2)
  const qx = px.slice(0, mid)
  const rx = px.slice(mid)
  const qy = Array.from({length: qx.length})
  const ry = Array.from({length: rx.length})

  const greatestQx = qx[qx.length - 1].x
  let i = 0
  let j = 0
  for (let k = 0; k < py.length; k++) {
    if (py[k].x < greatestQ) {
      qy[i] = py[k]
      i++
    } else {
      ry[j] = py[k]
      j++
    }
  }

  console.table({qx,rx,qy,ry})
}

const points = (function (numPoints) {
  const points = []
  while (numPoints > 0) {
    points.push({
      x: Math.floor(Math.random() * 15),
      y: Math.floor(Math.random() * 15),
    })
    numPoints--;
  }
  return points;
}(7))

const px = mergeSort(points, p => p.x)
const py = mergeSort(points, p => p.y)
closestPair(px, py)
```