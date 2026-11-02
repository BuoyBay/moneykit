---
title: "MoneyKit API"
summary: "Exact fixed-scale money arithmetic"
category: "Reference"
order: 10
keywords: ["moneykit", "Currency", "rounding"]
---

# MoneyKit 0.1.0

`Import moneykit` from the sealed `moneykit-0.1.0.buipkg` in a consumer's
`packages/` directory. No dependencies or FFI. All public methods are Shared
methods on `Money`; amounts and results are native `Currency` values.

| API | Contract |
| --- | --- |
| `Money.Round(amount, digits = 2, mode = HalfEven)` | Round to 0..4 fractional decimal digits; reject out-of-range result. |
| `Money.Format(amount, digits = 2, mode = HalfEven)` | Round first, then exact plain decimal text with exactly digits fractional places. No grouping, symbol, locale, exponent, or negative zero. |
| `Money.MultiplyRate(amount, numerator, denominator, mode = HalfEven)` | Exact rational multiplication, rounded once to one raw Currency unit (0.0001). Signed Int64 numerator/denominator; zero denominator throws. |
| `Money.Percent(amount, percentage, mode = HalfEven)` | Integer percentage, equivalent to MultiplyRate(amount, percentage, 100, mode). Fractional percentages use MultiplyRate, e.g. 7.5% is 75/1000. |
| `Money.Allocate(total, weights, digits = 4)` | Largest remainder allocation at 0..4 digits; total must already align to that precision. Fresh output; weights snapshotted. Positive integer weights only, 1..10000 entries, sum must fit positive Int64. |

`MoneyRoundingMode` is a separate enum: `HalfEven`, `HalfAway` (ties away
from zero), `TowardZero`, `Floor`, `Ceiling`. Invalid modes/digits, empty or
nonpositive weights, and a misaligned allocation total throw
`InvalidArgumentException`. Weight-sum or rounded-result overflow throws
`OverflowException`; zero rate denominator throws `DivideByZeroException`.
All numeric inputs accept the full signed Int64 domain, including minimum,
subject to these explicit result and weight bounds.

Allocation truncates each unsigned quota then awards residual units by descending
fractional remainder, with original index breaking ties. Negative totals receive
the negated positive-magnitude allocation, conserving the exact signed total.
No caller weights are modified. `Money.Allocate(Currency.FromInteger(100),
[1, 1, 1], 2)` gives 33.34/33.33/33.33; omit the precision argument for
33.3334/33.3333/33.3333. Precision is never inferred from an amount.

Arithmetic and formatting never convert to Double. Five base-32768 limbs per
operand and a bounded product feed exact binary long division. Checked signed
negative magnitudes support Int64 minimum and avoid spurious intermediate
product overflow; only the final rounded representability matters. Allocation
uses O(n²) deterministic remainder selection, bounded at 10000 weights; it is
intended for bill/share splits rather than large apportionment datasets.

Currency is fixed scale 10000 with raw signed Int64 storage, **not general
arbitrary-precision decimal**. No currency codes, exchange-rate source, locale,
parsing, arbitrary decimal arithmetic, financial/legal rounding compliance, or
cross-platform native-runtime conformance is supplied. Six-target semantic
checks establish compile-time portability only; native execution is tested on
Linux. See resources/buoy-docs and ../../examples/moneykit/main.bui.

Weights are validated for positivity before their sum is checked, so an invalid weight takes precedence over weight-sum overflow. `Money` and `MoneyRoundingMode` are the public names; the internal division helper is package-prefixed because this toolchain does not fully hide private class names across module imports.
