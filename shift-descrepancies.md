Doc. no.: Pxxxx  
Date: 2018-10-02  
Reply-to: Ashley Hedberg (ahedberg@google.com)  
Audience: LEWG/LWG

# Discrepancies between `expr.shift` and P0769R2

[`expr.shift`](http://eel.is/c++draft/expr.shift) defines the shift operators `<<` and `>>` for integral and unscoped enumeration types. [`P0769R2`](http://wg21.link/P0769R2) proposes function templates `shift_left` and `shift_right` for ranges. This paper identifies two discrepancies in what
behavior is defined for the two sets of shifts.

## Shift by negative

The behavior of `<<` and `>>` is undefined if the right operand is negative.
P0769R2 defines shifting a range by a negative `n` as a no-op in item (7) of the design decisions section.

## Shift by `n` greater than length

The behavior of `<<` and `>>` is undefined if the right operand is greater than or equal to the length in bits of the promoted left operand. P0769R2 defines shifting a range by more than its length as shifting the range by exactly its length.

## Suggested polls

Do we want the `shift_left` and `shift_right` to have the same (undefined) behavior as `expr.shift`?
