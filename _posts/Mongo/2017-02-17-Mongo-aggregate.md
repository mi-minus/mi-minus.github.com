---
layout: life
title: Mongo 聚合函数 Aggregate
category: Mongo
date: 2017-02-17
---

******

	作者: minus
	版本: V 0.0.1
	日期: 2017年2月17日

<!-- more -->

*******

### Mongo Aggregate

#### <font color=#8FBC8F>new aggregate.project change</font>
* adds support for field exclusion in the output document ( only exclude the _id field in the stage before)
    ```sh
    db.Tweets.aggregate([
    {
        '$project':{
                'Like':0   // (之前这个不可以，只有_id:0，　现在可以了)
            }
        }
    ])
    ```

#### New Aggregation Control Flow Expression 

* $switch : Evaluates, in sequential order, the case expressions of the specified branches to enter the first branch for which the case expression evaluates to true.
    ```sh
    $switch: {
       branches: [
         { case: <expression>, then: <expression> },
         { case: <expression>, then: <expression> },
         ...
      ],
      default: <expression>
    }
    ```

#### New Date Aggregation Operators

* $isoDayOfWeek : Returns the ISO 8601 weekday number, ranging from 1 (for Monday) to 7 (for Sunday).
    ```sh
    { $isoDayOfWeek: <date expression> }
    ```
    
* $isoWeek : Returns the ISO 8601 week number, which can range from 1 to 53. Week numbers start at 1 with the week (Monday through Sunday) that contains the year’s first Thursday.
    ```sh
    { $isoWeek: <date expression> }
    ```
    
* $isoWeekYear : Returns the ISO 8601 year number, where the year starts with the Monday of week 1 (ISO 8601) and ends with the Sundays of the last week (ISO 8601).
    ```sh
    { $isoWeekYear: <date expression> }
    ```

#### New Monitoring Aggregation Sources (监控性质)

* $collStats : Returns statistics regarding a collection or view.
   ```sh
    {
       $collStats:
       {
          latencyStats: { histograms: <boolean> },
          storageStats: {}
       }
    }
    ```
    
#### New Type Operator

* $type : Returns a string which specifies the BSON Types of the argument.
   ```sh
   { $type: <expression> }
   ```

#### New $Group operations

* $stdDevSamp : Calculates standard deviation
    ```sh
    { $stdDevSamp: <array> }
    ```
    
* $stdDevPop : Calculates population standard deviation
    ```sh
    { $stdDevPop: <array> }
    ```

#### New $Aggregation operations [https://docs.mongodb.com/manual/release-notes/3.2/#rel-notes-rs-enhancements]

* $sqrt : Calculates the square root.
    ```sh
    { $sqrt: <number> }
    ```
    
* $abs : Returns the absolute value of a number.
    ```sh
    { $abs: <number> }
    ```
    
* $log : Calculates the log of a number in the specified base
    ```sh
    { $log: [ <number>, <base> ] }
    ```
    
* $log10 : Calculates the log base 10 of a number.
    ```sh
    { $log10: <number> }
    ```
    
* $ln : Calculates the natural log of a number.
    ```sh
    { $ln: <number> }
    ```

* $pow : Raises a number to the specified exponent.
    ```sh
    { $pow: [ <number>, <exponent> ] }
    ```
    
* $exp : Raises e to the specified exponent.
   ```sh
   { exp: <number> }
   ```
   
* $trunc : Truncates a number to its integer.
    ```sh
    { $trunc: <number> }
    ```
    
* $ceil : Returns the smallest integer greater than or equal to the specified number
    ```sh
    { $ceil: <number> }
    ```
    
* $floor : Returns the largest integer less than or equal to the specified number
    ```sh
    { floor: <number> }
    ```

* $avg : 对数组内元素求平均值

* $ifNull 

#### New Aggregation Array Operators

* $slice : Returns a subset of an array.
    ```sh
    { $slice: [ <array>, <n> ] }
    { $slice: [ <array>, <position>, <n> ] }
    ```
    
* $arrayElemAt : Returns the element at the specified array index.
    ```sh
    { $arrayElemAt: [ <array>, <idx> ] }
    ```
    
* $concatArrays : Concatenates arrays.
    ```sh
    {
       $concatArrays: [ <array1>, <array2>, ... ]
    }
    ```
    
* $isArray : Determines if the operand is an array.
    ```sh
    { $isArray: [ <expression> ] }
    ```
    
* filter : Selects a subset of the array based on the condition
    ```sh
    {
       $filter:
       {
          input: <array>,
          as: <string>,
          cond: <expression>
       }
    }
    ```
    
* $in : Returns a boolean that indicates if a specified value is in an array.
    ```sh
    { $in: [ <expression>, <array expression> ] }
    ```
    
* $indexOfArray : Searches an array for an occurence of a specified value and returns the array index (zero-based) of the first occurence.
    ```sh
    { $indexOfArray: [ <array expression>, <search expression>, <start>, <end> ] }
    ```
    
* $range : Returns an array whose elements are a generated sequence of numbers.
    ```sh
    { $range: [ <start>, <end>, <non-zero step> ] }
    ```
 
 * $reverseArray : Returns an output array whose elements are those of the input array but in reverse order.
     ```sh
     { $reverseArray: <array expression> }
     ```
 
 * $reduce : Takes an array as input and applies an expression to each element in the array to return the final result of the expression.
     ```sh
     {
        $reduce: {
           input: <array>,
           initialValue: <expression>,
           in: <expression>
        }
     }
     ```
 
 * $zip : Returns an output array where each element is itself an array, consisting of elements in the corresponding array index position from the input arrays.
    ```sh
    {
       $zip: {
          inputs: [ <array expression1>,  ... ],
          useLongestLength: <boolean>,
          defaults:  <array expression>
        }
    }
    ```
 
#### New Aggregation String Operators

* $indexOfBytes : Searches a string for an occurence of a substring and returns the UTF-8 byte index (zero-based) of the first occurence.
  ```sh
  { $indexOfBytes: [ <string expression>, <substring expression>, <start>, <end> ] }
  ```

* $indexOfCP : Searches a string for an occurence of a substring and returns the UTF-8 code point index (zero-based) of the first occurence.
    ```sh
    { $indexOfCP: [ <string expression>, <substring expression>, <start>, <end> ] }
    ```
    
* $split : Splits a string by a specified delimiter into string components and returns an array of the string components.
    ```sh
    { $split: [ <string expression>, <delimiter> ] }
    ```
 
 * $strLenBytes : Returns the number of UTF-8 bytes for a string.
     ```sh
     { $strLenBytes: <string expression> }
     ```
     
* $strLenCP : Returns the number of UTF-8 code points for a string.
    ```sh
    { $strLenCP: <string expression> }
    ```
 
 * $substrBytes : Returns the substring of a string. The substring starts with the character at the specified UTF-8 byte index (zero-based) in the string for the length specified.
     ```sh
     { $substrBytes: [ <string expression>, <byte index>, <byte count> ] }
     ```
     
* $substrCP : Returns the substring of a string. The substring starts with the character at the specified UTF-8 code point index (zero-based) in the string for the length specified.
    ```sh
    { $substrCP: [ <string expression>, <code point index>, <code point count> ] }
    ```
 
#### Available in $project

* $avg

* $min

* $max

* $sum

* $stdDevPop

* $stdDevSamp
