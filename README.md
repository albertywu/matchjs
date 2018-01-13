# matchjs

A functional replacement for ES6 switch, without the bad parts

---

#### problems with [ES6 switch statement](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/switch)
- is not an expression, and cannot be assigned to a variable
- as a consequence, the semantics encourage side effects
- case fall-through is error-prone
- does not require that case statements cover the entire domain of possible expression values (leaky)
- case statements conditions lack flexibility of a function predicate (does a strict equality comparison with literals)

---

#### proposed API
```es6
match(expr)
  .case(p1, f1)
  .case(p2, f2)
  .case(p3, f3)
  .default(f4)
  
// pi is a predicate that takes expr as input and returns a boolean
// fi is an arbitrary function that gets invoked if pi yields true
```

---

#### example usage
```es6
const isTooHigh = x => x > 100
const isTooLow = x => x < 0
const x = getRandomInt()

const boundedValue = match(x)
  .case(isTooHigh, () => 100)
  .case(isTooLow, () => 0)
  .default(() => x)
```

---

#### typescript enhancements:
- type system should enforce that at least one `case` statement is specified
- something should enforce that the entire domain of possible `expr` is covered by predicates, and require that `default` is specified if not. This is to prevent bugs where an expression value might have no matching case.
- type script should infer the expression type (in the example above, should infer that `boundedValue` is type `number`
---

#### questions 
- is there a cleaner / more useful API that solves all problems above?
- are there any more constraints the typesystem could help with?
