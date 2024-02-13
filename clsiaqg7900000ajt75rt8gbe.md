---
title: "Learn Polyfill of JS Reduce with ChatGPT"
datePublished: Mon Feb 12 2024 02:09:32 GMT+0000 (Coordinated Universal Time)
cuid: clsiaqg7900000ajt75rt8gbe
slug: learn-polyfill-of-js-reduce-with-chatgpt
tags: javascript, reduce-method

---

```javascript
// callback -> previousValue, currentValue, index, array
function myReduce(callback, initialValue) {
    const array = this
    if(!array) throw new Error("Array is not defined")
    const arrayLength = this.length
    let index = 0
    
    if(!arrayLength) {
        if(!initialValue) throw new Error("You need to 
pass initial value if array is empty")
        return initialValue
    }
    let accumulator = initialValue ?? array[index++]
    while(index < arrayLength) {
        accumulator = callback(accumulator, array[index], index, array)
        index++
    }

    return accumulator
}

Array.prototype.myReduce = myReduce

const arr = undefined
const intValue = 1

const callback = (prev, currnt) => prev + currnt

console.log(arr.myReduce(callback, intValue))
```

**Me:** is this polyfill correct for js reduce?

**ChatGPT:** The provided polyfill for `Array.prototype.myReduce` looks generally correct. However, there are a few improvements and corrections that could be made:

1. **Checking for** `this` existence: Instead of checking if `array` is not `null` or `undefined`, it's better to use `if (!Array.isArray(this))` to check if `this` is indeed an array.
    
2. **Error messages**: Error messages should ideally provide more context. For instance, if `initialValue` is not provided when the array is empty, you should specify that in the error message.
    
3. **Checking for callback existence**: It's advisable to check if the `callback` function is provided.
    

Here's an updated version with these improvements:

```javascript
function myReduce(callback, initialValue) {
    if (!Array.isArray(this)) {
        throw new Error("myReduce can only be used on arrays.");
    }

    const array = this;
    const arrayLength = array.length;
    let index = 0;

    if (arrayLength === 0) {
        if (initialValue === undefined) {
            throw new Error("Reduce of empty array with no initial value.");
        }
        return initialValue;
    }

    if (typeof callback !== "function") {
        throw new TypeError("Callback must be a function.");
    }

    let accumulator = initialValue !== undefined ? initialValue : array[index++];

    while (index < arrayLength) {
        accumulator = callback(accumulator, array[index], index, array);
        index++;
    }

    return accumulator;
}

Array.prototype.myReduce = myReduce;

// Example usage
const arr = [1, 2, 3, 4];
const initialValue = 0;

const callback = (prev, current) => prev + current;

console.log(arr.myReduce(callback, initialValue)); // Output: 10
```

This updated version ensures better error handling and checks for `callback` existence, providing more robustness.  
  
Reference: [https://jscafe.dev/index.php/q14-polyfill-of-array-reduce/](https://jscafe.dev/index.php/q14-polyfill-of-array-reduce/)