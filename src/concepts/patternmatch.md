# Pattern Matching
Patterns take on many appearances, such as:

- Constants: `150`
- Variables: `x`
- Wildcard: `_`
- Tuples: `(true, _)`
- Constructors (which may contain other patterns):
    - Lists: `x::xs`
    - Other datatypes: `Node(L,x,R)`

Patterns can be matched against values to form bindings. In the following example, `1` gets bound to `x`, and `2` gets bound to `y`.

```val (x,y) = (1,2)```

Pattern matching may fail. For example, the following raises exception `Bind`.

```val 10 = 9```

Besides `val` declarations, pattern matching is also used in function declarations, lambda expressions, and case expressions.
## Function declarations:
```
fun fact 0 = 1
  | fact n = n * fact(n-1)
```

The function `fact` is given an `int` as input. If the input successfully matches the pattern `0`, then the function returns `1`. Otherwise, the input is matched with the pattern `n`, binding the input to `n`. For example, if we evaluate `fact 5`, then `5` is bound to `n`, so the expression becomes `5 * fact(4)`. 
    
Each clause of the function declaration tells `fact` what it should do, depending on the input. The bar, `|`, acts as a separator between the two clauses. 
    
Note that it's important for your patterns to be *exhaustive*. The above function is fine, because all values of type `int` can match with either `0` or `n`. However, suppose we had the following function:
```
fun fiction 1 = 1
  | fiction 2 = 2
  | fiction 3 = 6
```
There are many inputs which do not match with either `1`, `2`, or `3`. For example, `fiction 4` would raise exception `Match`.

## Lambda expressions:
```(fn [] => false | x::xs => true) [1,2,3]```

The lambda expression is similar to a function; as it turns an input into an output. In the example above, `[1,2,3]` is the input. It doesn't match with `[]`, but it does match with `x::xs`. Namely, `1` gets bound to `x`, and the list `[2,3]` gets bound to `xs`. As a result of this successful pattern matching, the lambda expression returns `true`. 
    
You should still make sure your patterns are exhaustive. For example, the following codeblock raises exception `Match`:

```(fn [] => false) [1,2,3]```

## Case expressions:
```
fun fact x =
    case x of
        0 => 1
      | n => n * fact (n-1)
```
First, note that this codeblock does the same thing as the example for function declarations. However, it uses an extra `case` expression.
    
Let's consider what happens when `fact` is given an input, like `5`. First, `5` gets bound to `x`. Then, the `case` expression tries to match `5` to a pattern. In this scenario, `5` successfully pattern matches with `n`, so `5` gets bound to `n`. Therefore, `fact 5` evaluates to `5 * fact(4)`. 
    
As usual, the patterns in `case` expressions should be exhaustive.
