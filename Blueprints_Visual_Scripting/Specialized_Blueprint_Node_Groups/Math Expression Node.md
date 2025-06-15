# Math Expression Node

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/math-expression-node-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/math-expression-node-in-unreal-engine)  
**Processed:** 2025-06-14 16:35:19

---

To create a Math Expression node, **Right-click** in the graph and select **Add Math Expression...** from the context menu.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8bf686b6-9dce-487b-bf4c-63e287764fe9/addmathexpression.png)

The Math Expression node acts like a collapsed graph. It is a single node that you can **Double-click** to open the sub-graph that makes up its functionality. Initially, the name/expression is blank. Whenever you rename the node, then the new expression is parsed and a new sub-graph is generated.

To rename the node and update the sub-graph, **Right-click** on the node and select **Rename**.

For example, you could rename the Math Expression node with the following expression:

```
	`(1+x)*sin(myVar)-2.4/rand()`

Copy full snippet
```
(1+x)\*sin(myVar)-2.4/rand()

This would update the Math Expression node to have two float inputs, **X** and **MyVar**, and one float output.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f44ed18c-0c2e-4aea-8c18-815b5850e7ee/mathnodeexample.png)

If you **Double-click** the node with this expression, you would see the below sub-graph:

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8c45a1c9-88ba-4363-9c82-47e671e24c86/mathnodeexpand.png)

The sub-graph is created by following the below rules:

1.  Alphabetic names (tokens beginning with a letter) should be turned into either variables, input pins on the Math Expression node, or function calls. From the example above: **x**, **sin**, **myVar**, and **rand**.
    1.  If an alphabetic name matches an existing variable in the Blueprint, then it will become a variable get node (i.e. if the Blueprint already had a **myVar** variable).
    2.  If an alphabetic name is followed by an open parenthesis, like **sin(** and **rand(**, then it will be turned into a function node.
    3.  If the previous two states are not met, then the alphabetic name is turned into a float input on the Math Expression node.
    4.  The name will also be used as an input if it matches the name of an existing pin on the node.
2.  Numerical constants are always turned into pin inputs. They never create a node themselves, but instead are used to fill out input fields on other nodes.
3.  Mathematical operators (like +, \*, -) are turned into function nodes.
4.  Like in mathematics, expressions inside of parentheses will take precedence, and be evaluated first.

## Variables

Variable naming is fairly flexible, but it is important to remember the following points:

-   Variables can have numbers in them, but they cannot start with a number.
-   Variables cannot have the same name as a hidden Blueprint variable.
-   Be sure that you are working with the correct type of variable. For example, **boolVar+1.5** is not a valid expression.

## Order of Operations

Operations follow the below order of operations (highest priority first):

1.  Parentheses
2.  Factorials
3.  Exponents
4.  Multiplication and division
5.  Addition and subtraction

## Available Blueprint Functions

Blueprint pure functions that are in a coded function library should all be available. These include:

-   Trig functions (sin/cos/tan, asin, acos, etc.):
    
    ```
              `sin(x)`
    Copy full snippet
    ```
    sin(x)
-   Clamping functions (min, max, clamp, etc.):
    
    ```
              `clamp(y,0,20)`
    Copy full snippet
    ```
    clamp(y,0,20)
-   Rounding functions (floor, fceil, round, etc.):
    
    ```
              `round(z)`
    Copy full snippet
    ```
    round(z)
-   Exponential functions (square, power, sqrt, loge, e/exp, etc.)
    

Certain functions have multiple names that are commonly used. To account for that, there are several aliases that map to the same function/node. Some examples are:

-   Power aliases: power, pow
-   Trig arc functions (asin/arcsin, acos/arccos, etc.)

Since you are typing in functions rather than connecting pins, make sure to enter the correct number and type of parameters. The Math Expression node will display an error if there is a mismatch.

## Basic Struct Types

There are some basic structures that we use quite often in math as well: vectors, transforms, etc. You can make and operate on these types in the expression easily.

-   The vector keyword spawns a MakeVector node:
    
    ```
              `vector(x,y,z)`
    Copy full snippet
    ```
    vector(x,y,z)
-   The rotator keyword spawns a MakeRotator node:
    
    ```
              `rotator(x,y,z)`
    Copy full snippet
    ```
    rotator(x,y,z)
-   The transform keyword spawns a MakeTransform node:
    
    ```
              `transform(vec(x,y,z), rot(p,y,r), vec(6,5,4))`
    		
    Copy full snippet
    ```
    transform(vec(x,y,z), rot(p,y,r), vec(6,5,4))

Just like there are aliases for certain functions, there are vector and rotator aliases.

-   Vector aliases
    
    ```
              `vector, vec, vect`
    Copy full snippet
    ```
    vector, vec, vect
-   Rotator aliases
    
    ```
              `rotator, rot`
    		
    Copy full snippet
    ```
    rotator, rot

## Supported Operators

The following operators should all be supported, and the logical and comparison operators can be combined to create complex expressions.

-   Multiplicative:
    
    ```
              `*, /, %`
    Copy full snippet
    ```
    \*, /, %
-   Additive:
    
    ```
              `+, -`
    Copy full snippet
    ```
    +, -
-   Relational:
    
    ```
              `<, >, <=, >=`
    Copy full snippet
    ```
    <, >, <=, >=
-   Equality:
    
    ```
              `==, !=`
    Copy full snippet
    ```
    \==, !=
-   Logical:
    
    ```
              `||, &&, ^`
    		
    Copy full snippet
    ```
    ||, &&, ^

## Unsupported Operators

Currently, the following operators are unsupported.

-   Conditional:
    
    ```
              `?:`
    Copy full snippet
    ```
    ?:
-   Bitwise:
    
    ```
              `|, &, <<, >>`
    Copy full snippet
    ```
    |, &, <<, >>
-   Unary prefix:
    
    ```
              `+, -, ++, --, ~, !, etc.`
    Copy full snippet
    ```
    +, -, ++, --, ~, !, etc.
-   Postfix:
    
    ```
              `++, --, [], etc.`
    Copy full snippet
    ```
    ++, --, \[\], etc.