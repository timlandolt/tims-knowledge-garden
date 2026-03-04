---
{"dg-publish":true,"permalink":"/knowledge/code-coverage/","tags":["testing","unit-testing","code-coverage"]}
---

---

Percentage of code that gets executed when a test suite is run. There are four common criterias to measure/define the coverage.

- Function Coverage
- Statement Coverage
- Branch Coverage
- Condition Coverage Criteria

## Coverage Criteria

### Function Coverage
Has every function/method/subroutine of the program been called?

### Statement Coverage
Has every statement been executed?

### Branch Coverage
Has every branch of every control flow structure been executed (if else, switch, while, ...)

```rb
if cond1 && cond2
	puts "Smaller"
else
	puts "Greater"
endif
```

**Test data that would pass**

| cond1 | cond2 |
| ----- | ----- |
| true  | true  |
| true  | false |

### Condition Coverage
Has every boolean sub-expression been evaluated true and false

```rb
if cond1 && cond2
	puts "Smaller"
else
	puts "Greater"
endif
```

| cond1 | cond2 |
| ----- | ----- |
| true  | true  |
| true  | false |
| false | false |
| false | true  |

## In practice

Line(=statement) coverage and Branch coverage are the two most common forms of test coverage.
Statement coverage is also called C1 and Branch coverage C2. With a combination of C1 and C2 you get a total coverage of nearly 100%.