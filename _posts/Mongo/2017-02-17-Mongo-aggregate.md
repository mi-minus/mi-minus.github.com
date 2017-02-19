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

#### New $Group operations

* $stdDevSamp : Calculates standard deviation
    ```
    { $stdDevSamp: <array> }
    ```
* $stdDevPop : Calculates population standard deviation
    ```
    { $stdDevPop: <array> }
    ```

#### New $Aggregation operations [https://docs.mongodb.com/manual/release-notes/3.2/#rel-notes-rs-enhancements]

* $sqrt : Calculates the square root.
    ```
    { $sqrt: <number> }
    ```
    
* $abs : Returns the absolute value of a number.
    ```
    { $abs: <number> }
    ```
    
* $log : Calculates the log of a number in the specified base
    ```
    { $log: [ <number>, <base> ] }
    ```
    
* $log10 : Calculates the log base 10 of a number.
    ```
    { $log10: <number> }
    ```
    
* $ln : Calculates the natural log of a number.
    ```
    { $ln: <number> }
    ```

* $pow : Raises a number to the specified exponent.
    ```
    { $pow: [ <number>, <exponent> ] }
    ```
    
* $exp : Raises e to the specified exponent.
   ```
   { exp: <number> }
   ```
   
* $trunc : Truncates a number to its integer.
    ```
    { $trunc: <number> }
    ```
    
* $ceil : Returns the smallest integer greater than or equal to the specified number
    ```
    { $ceil: <number> }
    ```
    
* $floor : Returns the largest integer less than or equal to the specified number
    ```
    { floor: <number> }
    ```

#### New Aggregation Array Operators

* $slice : Returns a subset of an array.
    ```
    { $slice: [ <array>, <n> ] }
    { $slice: [ <array>, <position>, <n> ] }
    ```
    
* $arrayElemAt : Returns the element at the specified array index.
    ```
    { $arrayElemAt: [ <array>, <idx> ] }
    ```
    
* $concatArrays : Concatenates arrays.
    ```
    {
       $concatArrays: [ <array1>, <array2>, ... ]
    }
    ```
    
* $isArray : Determines if the operand is an array.
    ```
    { $isArray: [ <expression> ] }
    ```
    
* filter : Selects a subset of the array based on the condition
    ```
    {
       $filter:
       {
          input: <array>,
          as: <string>,
          cond: <expression>
       }
    }
    ```
    
#### Available in $project

* $avg
* $min
* $max
* $sum
* $stdDevPop
* $stdDevSamp
