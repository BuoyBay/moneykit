---
title: "Getting started"
summary: "Exact fixed-scale money arithmetic"
category: "Reference"
order: 10
keywords: ["moneykit", "Currency", "rounding"]
---

Put moneykit-0.1.0.buipkg in packages/. The standalone example is examples/moneykit/main.bui. Allocate 100 with weights [1,1,1] and digits 2 for 33.34/33.33/33.33.


Save the following as `main.bui` in your consumer project. Package archives and any dependencies must be installed as described above.

```buoy
Import moneykit

Sub Main()
    Dim total As Currency = Currency.FromInteger(100)
    Dim parts As Array Of Currency = Money.Allocate(total, [1, 1, 1], 2)
    For Each part As Currency In parts
        Print Money.Format(part, 2)
    Next
    Print Money.Format(Money.Percent(total, 7), 2)
End Sub
```
