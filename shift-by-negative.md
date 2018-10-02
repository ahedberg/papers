Doc. no.: Dxxxx  
Date: 2018-10-02  
Reply-to: Ashley Hedberg (ahedberg@google.com), Matt Calabrese (metaprogrammingtheworld@gmail.com)  
Audience: LEWG/LWG

# Shift-by-negative in `shift_left` and `shift_right`

[`P0769R2`](http://wg21.link/P0769R2) was applied to the C++ working paper in
Rapperswil. That paper defines shifting a range by a negative `n` as a no-op in
item (7) of the design decisions section. This is surprising for two reasons:

-   [`expr.shift`](http://eel.is/c++draft/expr.shift) places a different precondition on the shift operators `<<` and `>>`: the right operand must be greater than or equal to 0.

-   The [LWG discussion notes](http://wiki.edg.com/bin/view/Wg21rapperswil2018/LWGP0769) on P0769R2 suggest that there are APIs which perform a left-shift when invoking `shift_right` with a negative `n`, and perform a right-shift when invoking `shift_left` with a negative `n`. One example is [perlop](http://shortn/_Uz897VKAPn).

The current treatment of a negative shift as a shift of 0 seems unlikely to match user intent and may hide bugs. If the programmer explicitly wrote a negative value, they probably didn't expect a shift of 0. If the user specified a negative shift as the result of some programmatic calculation, it is likely that the calculation was incorrect, or that a shift in the opposite direction would be the correct behavior. Either way, implicitly shifting by 0 feels questionable.

We propose that this case be a precondition violation instead: `shift_left` and `shift_right` should require that `n` be a nonnegative number.

## Suggested poll

Do we want the `shift_left` and `shift_right` algorithms to have a precondition that the value of `n` must be greater than or equal to 0?
