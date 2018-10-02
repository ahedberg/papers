Doc. no.: Dxxxx  
Date: 2018-10-02  
Reply-to: Ashley Hedberg (ahedberg@google.com)  
Audience: LEWG/LWG

# Shift-by-negative in `shift_left` and `shift_right`

[`P0769R2`](http://wg21.link/P0769R2) was applied to the C++ working paper in
Rapperswil. That paper defines shifting a range by a negative `n` as a no-op in
item (7) of the design decisions section. This is surprising for two reasons:

-   [`expr.shift`](http://eel.is/c++draft/expr.shift) places a different precondition on the shift operators `<<` and `>>`: the right operand must be greater than or equal to 0.

-   One could expect that invoking `shift_right` with a negative `n` would perform a left-shift, and that invoking `shift_left` with a negative `n` would perform a right-shift. The [LWG discussion notes](http://wiki.edg.com/bin/view/Wg21rapperswil2018/LWGP0769) on P0769R2 suggest that there are APIs which do this; [perlop](http://shortn/_Uz897VKAPn) is one.

For the sake of consistency, this paper proposes that `shift_left` and `shift_right` maintain the same precondition as `<<` and `>>`, and require that `n` be a nonnegative number.

## Suggested poll

Do we want the `shift_left` and `shift_right` algorithms to have a precondition that the value of `n` must be greater than or equal to 0?
