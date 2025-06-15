# BuildGraph Script Conditions

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/buildgraph-script-conditions-reference-for-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/buildgraph-script-conditions-reference-for-unreal-engine)  
**Processed:** 2025-06-14 16:11:22

---

If you want to build logical complexity into your **BuildGraph** scripts, you need to work with **conditionals**. The following section introduces you to how BuildGraph conditions are written, including a list of conditional operators.

## Conditions

BuildGraph script conditions consist of atoms and operators that evaluate to `true` or `false`.

### Atoms

**Atoms** can be numbers, strings, or identifiers that are coerced to their appropriate type for the operator using them. Atoms may be quoted with single (') or double (") quotes. They can also be an unquoted sequence of letters, digits, and underscore characters. All atoms are considered the same type, regardless of how they are declared. Additionally, atoms are considered case-insensitive for comparisons. This means that the strings "True" and 'true' are identical to the identifier `true` (despite the presence of quotes and differences in case).

## Operators

A list of operators is specified below:

| **Operator** | **Description** | **Precedence** |
| --- | --- | --- |
| `(x)` | Subexpression used for grouping. | 1 |
| `!x` | Evaluates to `true` if `x` is `false`. | 1 |
| `Exists(x)` | Evaluates to `true` if the file `x` exists. | 1 |
| `HasTrailingSlash(x)` | Evaluates to `true` if `x` ends with a slash or backslash. | 1 |
| `x == y` | Evaluates to `true` if the two atoms are equal (case insensitive). | 2 |
| `x != y` | Evaluates to `true` if the two atoms are not equal (case insensitive). | 2 |
| `x < y` | Evaluates to `true` if the integer `x` is less than the integer `y`. | 2 |
| `x <= y` | Evaluates to `true` if the integer `x` is less than or equal to the integer `y`. | 2 |
| `x > y` | Evaluates to `true` if the integer `x` is greater than the integer `y`. | 2 |
| `x >= y` | Evaluates to `true` if the integer `x` is greater than or equal to the integer `y`. | 2 |
| `x and y` | Evaluates to `true` if both atoms are `true`. | 3 |
| `x or y` | Evaluates to `true` if either `x` is `true`, `y` is `true`, or both atoms are `true`. | 4 |

The `'<'` and `'>'` characters must be escaped as `"<"` and `">"` in XML.