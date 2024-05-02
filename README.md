# Problem Solving - Divide and Conquer
### Binary Search Algorithms
+ Additional Test Cases added
+ TODO: findRotatedIndex 2*O(log*n) implementation
---
### countZeroes
```javascript
function countZeroes(arr){
    let low = 0;
    let high = arr.length;
    while(low <= high) {
        let mid = low + Math.floor((high - low) / 2);
        if (arr[mid] === 0 && (mid === 0 || arr[mid - 1] === 1))
            return arr.length - mid;
        else if (arr[mid] === 1) {
            low = mid + 1;
            continue;
        }
        high = mid - 1;
    }
    return 0;
}
countZeroes([1, 0, 0, 0, 0]) // 4
countZeroes([0, 0, 0]) // 3
countZeroes([1, 1, 1, 1]) // 0
countZeroes([1, 1, 1, 1, 0, 0]) // 2
countZeroes([]) // 0 (empty array)
countZeroes([1, 1, 1, 1]) // 0
countZeroes([1, 1, 1, 1, 0, 0]) // 2
countZeroes([1, 0, 0, 0, 0]) // 4
countZeroes([0, 0, 0]) // 3
countZeroes([1, 1, 1, 0, 0, 0, 0]) // 4
countZeroes([1, 1, 1, 1, 1, 0, 0, 0, 0]) // 4
countZeroes([1, 0, 0, 0, 0, 0, 0]) // 6
countZeroes([1, 1, 0, 0, 0, 0, 0]) // 5
countZeroes([1, 1, 0, 0]) // 2
```
---
### sortedFrequency
```javascript
function sortedFrequency(arr, val) {
    let low = 0;
    let high = arr.length;
    let lowest = 0;
    while (low <= high) {
        let mid = low + Math.floor((high - low) / 2);
        if (arr[mid] === val && (mid === 0 || arr[mid - 1] != val)) {
            lowest = mid; 
            low = lowest; 
            high = arr.length;
            //Find right
            while (low <= high) {
                mid = low + Math.floor((high - low) / 2);
                if ((mid === arr.length - 1  || arr[mid + 1] != val) &&
                    arr[mid] === val) {
                    return mid - lowest + 1;
                } else if (arr[mid] <= val) {
                    low = mid + 1;
                    continue;
                }
                high = mid - 1;
            }
            return -1;
        } else if (arr[mid] >= val) {
            high = mid - 1;
            continue;
        }
        low = mid + 1;
    }
    return -1;
}
sortedFrequency([1, 1, 2, 2, 2, 2, 3], 2) // 4
sortedFrequency([1, 1, 2, 2, 2, 2, 3], 3) // 1
sortedFrequency([1, 1, 2, 2, 2, 2, 3], 1) // 2
sortedFrequency([1, 1, 2, 2, 2, 2, 3], 4) // -1
sortedFrequency([1, 2, 3, 4, 5], 3) // 1
sortedFrequency([1, 2, 3, 4, 5], 6) // -1
sortedFrequency([1, 1, 1, 1, 1], 1) // 5
sortedFrequency([], 1) // -1
sortedFrequency([1, 2, 2, 3, 3, 3, 4, 4, 4, 4], 4) // 4
sortedFrequency([1, 1, 2, 3, 3, 3, 4, 5, 5], 3) // 3
sortedFrequency([1, 2, 2, 2, 3, 4, 5, 5, 5, 5, 6], 5); // 4
sortedFrequency([1, 1, 1, 1, 2, 2, 3, 3, 3, 3, 3, 4, 4, 5, 5, 6, 6, 6], 3); // 5
sortedFrequency([1, 1, 2, 3, 3, 4, 5, 5, 6, 7, 8, 9, 9, 9, 9, 9], 9); // 5
sortedFrequency([1, 1, 1, 1, 1, 1, 1, 1, 1], 1); // 9
sortedFrequency([1, 2, 3, 4, 5, 6, 7, 8, 9], 10); // -1
sortedFrequency([1, 1, 2, 2, 3, 3, 4, 4, 5, 5, 6, 6, 7, 7, 8], 5); // 2
sortedFrequency([2, 3, 3, 4, 4, 4, 5, 5, 5, 6, 6, 6, 7, 7, 8], 4); // 3
sortedFrequency([1, 1, 2, 3, 3, 3, 4, 4, 4, 5, 5, 5, 6, 6, 6], 6); // 3
sortedFrequency([1, 1, 2, 2, 2, 3, 3, 4, 4, 5, 5, 6, 6, 7, 7], 2); // 3
sortedFrequency([1, 1, 1, 2, 2, 3, 3, 4, 4, 5, 5, 6, 6, 7, 7], 1); // 3
```
---
### findRotatedIndex
```javascript
function findRotatedIndex(arr, val) {
    let left = 0;
    let right = arr.length - 1;
    while (left <= right) {
        let mid = left + Math.floor((right - left) / 2);
        if (arr[mid] === val)
            return mid;
        if (arr[left] <= arr[mid])
            if (arr[left] <= val && val < arr[mid])
                right = mid - 1;
            else
                left = mid + 1;
        else
            if (arr[mid] < val && val <= arr[right])
                left = mid + 1;
            else
                right = mid - 1;
    }
    return -1;
}
findRotatedIndex([10, 11, 12, 14, 15, 16, 18, 2, 3, 4, 5, 6, 7, 8, 9], 18); // 6
findRotatedIndex([10, 11, 12, 14, 15, 16, 18, 2, 3, 4, 5, 6, 7, 8, 9], 18); //6
findRotatedIndex([3, 4, 1, 2], 4) // 1
findRotatedIndex([6, 7, 8, 9, 1, 2, 3, 4], 8) // 2
findRotatedIndex([6, 7, 8, 9, 1, 2, 3, 4], 3) // 6
findRotatedIndex([37, 44, 66, 102, 10, 22], 14) // -1
findRotatedIndex([6, 7, 8, 9, 1, 2, 3, 4], 12) // -1
findRotatedIndex([2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 14, 15, 16, 18], 2); // 0
findRotatedIndex([5, 6, 7, 8, 9, 10, 11, 12, 14, 15, 16, 18, 2, 3, 4], 4); // 14
findRotatedIndex([1, 2, 3, 5, 6, 7, 8, 9, 10, 11, 12, 14, 15, 16, 18], 20); //-1
findRotatedIndex([11, 12, 14, 15, 16, 18, 2, 3, 4, 5, 6, 7, 8, 9, 10], 10); //14
```
---
### findRotationCount
```javascript
function findRotationCount(arr) {
    let left = 0;
    let right = arr.length - 1;
    if (arr[left] <= arr[right])
        return 0;
    while (left <= right) {
        let mid = left + Math.floor((right - left) / 2);
        if (arr[mid] > arr[mid + 1]) {
            return mid + 1;
        } else if (arr[mid] >= arr[left]) {
            left = mid + 1;
            continue;
        }
        right = mid - 1;
    }
    return 0;
}
findRotationCount([15, 18, 2, 3, 6, 12]) // 2
findRotationCount([7, 9, 11, 12, 5]) // 4
findRotationCount([7, 9, 11, 12, 15]) // 0
findRotationCount([3, 4, 5, 6, 7, 8, 9, 1, 2]) // 7
findRotationCount([4, 5, 6, 7, 0, 1, 2]) // 4
findRotationCount([2, 3, 4, 5, 6, 1]) // 5
findRotationCount([1, 2, 3, 4, 5]) // 0
findRotationCount([5, 1, 2, 3, 4]) // 1
```
---
### findFloor
```javascript
function findFloor(arr, val) {
    let left = 0;
    let right = arr.length - 1;
    if (val < arr[left])
        return -1;
    while (left <= right) {        
        let mid = left + Math.floor((right - left) / 2);
        //console.log("new mid " + mid + " arr[mid] is " + arr[mid]);
        if (arr[mid] == val && arr[mid+1] > val) {
            return arr[mid];
        } else if (arr[mid] < val && arr[mid + 1] > val) {
            //console.log(arr[mid] + " > " + val + " > " + arr[mid - 1]);
            return arr[mid];
        } else if (arr[mid] > val) {
            //console.log("move to left " + arr[mid] + "->" + arr[mid - 1]);
            right = mid - 1;
        } else {
            //console.log("move to right " + arr[mid] + "->" + arr[mid + 1]);
            left = mid + 1;
        }
    }
    return arr[arr.length - 1];
}
findFloor([1, 2, 8, 10, 10, 12, 19], 19) // 19
findFloor([1, 2, 8, 10, 10, 12, 19], 1) // 1
findFloor([1, 2, 8, 10, 10, 12, 19], 0) // -1
findFloor([1, 2, 8, 10, 10, 12, 19], -5) // -1
findFloor([], 5) // -1
findFloor([7], 5) // -1
findFloor([1, 2, 3, 4, 5], 10) // 5
findFloor([10, 20, 30, 40, 50], 5) // -1
findFloor([1, 2, 3, 4, 5], 1) // 1
findFloor([1, 2, 3, 4, 5], 5) // 5
findFloor([1, 2, 2, 3, 3, 4, 5], 3) // 3 
findFloor([1, 2, 8, 10, 10, 12, 19], 7) // 2
findFloor([1, 2, 8, 10, 10, 12, 19], 9) // 8
findFloor([1, 2, 8, 10, 10, 12, 19], 20) // 19
findFloor([1, 2, 8, 10, 10, 12, 19], 11) // 10
findFloor([1, 2, 8, 10, 10, 12, 19], 10) // 10
findFloor([1, 2, 8, 10, 10, 12, 19], 20) // 19
```
