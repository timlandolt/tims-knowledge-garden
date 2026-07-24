---
{"dg-publish":true,"permalink":"/knowledge/abc-metric/","tags":["metric","code-quality"]}
---

---

The ABC score is a triplet of values that represent the size of a code segment (e.g. a method).

It consists of the following counts:
- **A**ssignment => Variables
- **B**ranches => Method calls
- **C**onditionals => Boolean and logic tests

In addition, a singular Value can be counted as following:

$$
|ABC| = \sqrt{A^{2} + B^{2} + C^{2}}
$$


```rb
def order_summary(order)
  total = 0                          # Assignment (A)
  discount = 0                       # Assignment (A)

  if order.vip?                      # Condition (C)
    discount = total * 0.1           # Assignment (A)
  end

  order.items.each do |item|         # Branch (B) - calling .each
    total += item.price              # Assignment (A)
  end

  total -= discount                  # Assignment (A)

  puts "Total: #{total}"             # Branch (B) - calling puts
  logger.info("Order processed")     # Branch (B) - calling logger.info

  total > 0 ? total : 0              # Condition (C) - ternary
end
```

$$ABC =< 5, 3, 2 >$$
$$\sqrt{5^{2} + 3^{2} + 2^{2}} ≈ 6.2$$
