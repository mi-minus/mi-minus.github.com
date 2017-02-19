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

#### <font color="#1C86EE">new aggregate.project change</font>
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

#### <font color="#1C86EE">new aggregate count</font>
* <font color="#7EC0EE">$count</font> : Returns a document that contains a count of the number of documents input to the stage.
    ```sh
	db.scores.aggregate(
	  [
	    {
	      $match: {
		score: {
		  $gt: 80
		}
	      }
	    },
	    {
	      $count: "passing_scores"
	    }
	  ]
	)
    ```

#### <font color="#1C86EE">[$graphLookup - new aggregate stage](https://docs.mongodb.com/manual/reference/operator/aggregation/graphLookup/)</font>
* <font color="#7EC0EE">$graphLookup</font> : Performs a recursive search on a collection, with options for restricting the search by recursion depth and query filter
    ```
    {
     $graphLookup: {
        from: <collection>,
        startWith: <expression>,
        connectFromField: <string>,
        connectToField: <string>,
        as: <string>,
        maxDepth: <number>,
        depthField: <string>,
        restrictSearchWithMatch: <document>
      }
    }
    ```
    

* $graphLookup注意事项
    1. The collection specified in from cannot be sharded.
    2. Setting the maxDepth field to 0 is equivalent to a non-recursive $lookup search stage.
    3. $graphLookup cannot use disk space as memory the way other aggregation operations can

* <font color="#7EC0EE">$sortByCount</font> : The operation returns the following documents, sorted in descending order by count
    ```
    { $sortByCount:  <expression> }
    db.exhibits.aggregate( [ { $unwind: "$tags" },  { $sortByCount: "$tags" } ] )
    ```

#### <font color="#1C86EE">New Aggregation Control Flow Expression</font>

* <font color="#7EC0EE">$switch</font> : Evaluates, in sequential order, the case expressions of the specified branches to enter the first branch for which the case expression evaluates to true.
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

#### <font color="#1C86EE">New Date Aggregation Operators</font>

* <font color="#7EC0EE">$isoDayOfWeek</font> : Returns the ISO 8601 weekday number, ranging from 1 (for Monday) to 7 (for Sunday).
    ```sh
    { $isoDayOfWeek: <date expression> }
    ```
    
* <font color="#7EC0EE">$isoWeek</font> : Returns the ISO 8601 week number, which can range from 1 to 53. Week numbers start at 1 with the week (Monday through Sunday) that contains the year’s first Thursday.
    ```sh
    { $isoWeek: <date expression> }
    ```
    
* <font color="#7EC0EE">$isoWeekYear</font> : Returns the ISO 8601 year number, where the year starts with the Monday of week 1 (ISO 8601) and ends with the Sundays of the last week (ISO 8601).
    ```sh
    { $isoWeekYear: <date expression> }
    ```

#### <font color="#1C86EE">New Monitoring Aggregation Sources (监控性质)</font>

* <font color="#7EC0EE">$collStats</font> : Returns statistics regarding a collection or view.
   ```sh
    {
       $collStats:
       {
          latencyStats: { histograms: <boolean> },
          storageStats: {}
       }
    }
    ```
    
#### <font color="#1C86EE">New Type Operator</font>

* <font color="#7EC0EE">$type</font> : Returns a string which specifies the BSON Types of the argument.
   ```sh
   { $type: <expression> }
   ```

#### <font color="#1C86EE">New $Group operations</font>

* <font color="#7EC0EE">$stdDevSamp</font> : Calculates standard deviation
    ```sh
    { $stdDevSamp: <array> }
    ```
    
* <font color="#7EC0EE">$stdDevPop</font> : Calculates population standard deviation
    ```sh
    { $stdDevPop: <array> }
    ```

#### <font color="#1C86EE">New $Aggregation operations</font> [https://docs.mongodb.com/manual/release-notes/3.2/#rel-notes-rs-enhancements]

* <font color="#7EC0EE">$sqrt</font> : Calculates the square root.
    ```sh
    { $sqrt: <number> }
    ```
    
* <font color="#7EC0EE">$abs</font> : Returns the absolute value of a number.
    ```sh
    { $abs: <number> }
    ```
    
* <font color="#7EC0EE">$log</font> : Calculates the log of a number in the specified base
    ```sh
    { $log: [ <number>, <base> ] }
    ```
    
* <font color="#7EC0EE">$log10</font> : Calculates the log base 10 of a number.
    ```sh
    { $log10: <number> }
    ```
    
* <font color="#7EC0EE">$ln</font> : Calculates the natural log of a number.
    ```sh
    { $ln: <number> }
    ```

* <font color="#7EC0EE">$pow</font> : Raises a number to the specified exponent.
    ```sh
    { $pow: [ <number>, <exponent> ] }
    ```
    
* <font color="#7EC0EE">$exp</font> : Raises e to the specified exponent.
   ```sh
   { exp: <number> }
   ```
   
* <font color="#7EC0EE">$trunc</font> : Truncates a number to its integer.
    ```sh
    { $trunc: <number> }
    ```
    
* <font color="#7EC0EE">$ceil</font> : Returns the smallest integer greater than or equal to the specified number
    ```sh
    { $ceil: <number> }
    ```
    
* <font color="#7EC0EE">$floor</font> : Returns the largest integer less than or equal to the specified number
    ```sh
    { floor: <number> }
    ```

* <font color="#7EC0EE">$avg</font> : 对数组内元素求平均值

* <font color="#7EC0EE">$ifNull</font>

#### <font color="#1C86EE">New Aggregation Array Operators</font>
* <font color="#7EC0EE">$slice</font> : Returns a subset of an array.
    ```sh
    { $slice: [ <array>, <n> ] }
    { $slice: [ <array>, <position>, <n> ] }
    ```
    
* <font color="#7EC0EE">$arrayElemAt</font> : Returns the element at the specified array index.
    ```sh
    { $arrayElemAt: [ <array>, <idx> ] }
    ```
    
* <font color="#7EC0EE">$concatArrays</font> : Concatenates arrays.
    ```sh
    {
       $concatArrays: [ <array1>, <array2>, ... ]
    }
    ```
    
* <font color="#7EC0EE">$isArray</font> : Determines if the operand is an array.
    ```sh
    { $isArray: [ <expression> ] }
    ```
    
* <font color="#7EC0EE">$filter</font> : Selects a subset of the array based on the condition
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
    
* <font color="#7EC0EE">$in</font> : Returns a boolean that indicates if a specified value is in an array.
    ```sh
    { $in: [ <expression>, <array expression> ] }
    ```
    
* <font color="#7EC0EE">$indexOfArray</font> : Searches an array for an occurence of a specified value and returns the array index (zero-based) of the first occurence.
    ```sh
    { $indexOfArray: [ <array expression>, <search expression>, <start>, <end> ] }
    ```
    
* <font color="#7EC0EE">$range</font> : Returns an array whose elements are a generated sequence of numbers.
    ```sh
    { $range: [ <start>, <end>, <non-zero step> ] }
    ```
 
 * <font color="#7EC0EE">$reverseArray</font> : Returns an output array whose elements are those of the input array but in reverse order.
     ```sh
     { $reverseArray: <array expression> }
     ```
 
 * <font color="#7EC0EE">$reduce</font> : Takes an array as input and applies an expression to each element in the array to return the final result of the expression.
     ```sh
     {
        $reduce: {
           input: <array>,
           initialValue: <expression>,
           in: <expression>
        }
     }
     ```
 
 * <font color="#7EC0EE">$zip</font> : Returns an output array where each element is itself an array, consisting of elements in the corresponding array index position from the input arrays.
    ```sh
    {
       $zip: {
          inputs: [ <array expression1>,  ... ],
          useLongestLength: <boolean>,
          defaults:  <array expression>
        }
    }
    ```
 
#### <font color="#1C86EE">New Aggregation String Operators</font>

* <font color="#7EC0EE">$indexOfBytes</font> : Searches a string for an occurence of a substring and returns the UTF-8 byte index (zero-based) of the first occurence.
  ```sh
  { $indexOfBytes: [ <string expression>, <substring expression>, <start>, <end> ] }
  ```

* <font color="#7EC0EE">$indexOfCP</font> : Searches a string for an occurence of a substring and returns the UTF-8 code point index (zero-based) of the first occurence.
    ```sh
    { $indexOfCP: [ <string expression>, <substring expression>, <start>, <end> ] }
    ```
    
* <font color="#7EC0EE">$split</font> : Splits a string by a specified delimiter into string components and returns an array of the string components.
    ```sh
    { $split: [ <string expression>, <delimiter> ] }
    ```
 
 * <font color="#7EC0EE">$strLenBytes</font> : Returns the number of UTF-8 bytes for a string.
     ```sh
     { $strLenBytes: <string expression> }
     ```
     
* <font color="#7EC0EE">$strLenCP</font> : Returns the number of UTF-8 code points for a string.
    ```sh
    { $strLenCP: <string expression> }
    ```
 
 * <font color="#7EC0EE">$substrBytes</font> : Returns the substring of a string. The substring starts with the character at the specified UTF-8 byte index (zero-based) in the string for the length specified.
     ```sh
     { $substrBytes: [ <string expression>, <byte index>, <byte count> ] }
     ```
     
* <font color="#7EC0EE">$substrCP</font> : Returns the substring of a string. The substring starts with the character at the specified UTF-8 code point index (zero-based) in the string for the length specified.
    ```sh
    { $substrCP: [ <string expression>, <code point index>, <code point count> ] }
    ```
 
#### <font color="#1C86EE">Available in $project</font>
* <font color="#7EC0EE">$avg</font>

* <font color="#7EC0EE">$min</font>

* <font color="#7EC0EE">$max</font>

* <font color="#7EC0EE">$sum</font>

* <font color="#7EC0EE">$stdDevPop</font>

* <font color="#7EC0EE">$stdDevSamp</font>
