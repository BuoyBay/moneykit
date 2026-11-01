---
title: "moneykit typed API"
summary: "Source-derived public signatures, properties, parameters, defaults, and return values."
category: "Reference"
order: 21
types: ["Money", "MoneyRoundingMode"]
dependencies: []
symbols: ["Money", "MoneyRoundingMode"]
related: ["api.md", "getting-started.md", "index.md"]
---

# moneykit typed API

Generated from the package source declarations. Platform guards are shown where present; inherited members are documented on the base type. See the [API contracts](api.md) for behavior and limitations.

## MoneyRoundingMode

`Public Enum MoneyRoundingMode As Integer`

### Values

| Name | Type | Value / Default | Description |
| --- | --- | --- | --- |
| `HalfEven` | `MoneyRoundingMode` | `0` | — |
| `HalfAway` | `MoneyRoundingMode` | `1` | — |
| `TowardZero` | `MoneyRoundingMode` | `2` | — |
| `Floor` | `MoneyRoundingMode` | `3` | — |
| `Ceiling` | `MoneyRoundingMode` | `4` | — |

## Money

`Public Class Money`

Exact fixed-scale Currency utilities. No floating-point arithmetic.

### MultiplyRate

`Public Shared Function MultiplyRate(amount As Currency, numerator As Integer, denominator As Integer, mode As MoneyRoundingMode = MoneyRoundingMode.HalfEven) As Currency`

#### Parameters

| Name | Type | Passing | Default |
| --- | --- | --- | --- |
| `amount` | `Currency` | `ByVal` | Required |
| `numerator` | `Integer` | `ByVal` | Required |
| `denominator` | `Integer` | `ByVal` | Required |
| `mode` | `MoneyRoundingMode` | `ByVal` | `MoneyRoundingMode.HalfEven` |

#### Returns

| Type |
| --- |
| `Currency` |

### Percent

`Public Shared Function Percent(amount As Currency, percentage As Integer, mode As MoneyRoundingMode = MoneyRoundingMode.HalfEven) As Currency`

#### Parameters

| Name | Type | Passing | Default |
| --- | --- | --- | --- |
| `amount` | `Currency` | `ByVal` | Required |
| `percentage` | `Integer` | `ByVal` | Required |
| `mode` | `MoneyRoundingMode` | `ByVal` | `MoneyRoundingMode.HalfEven` |

#### Returns

| Type |
| --- |
| `Currency` |

### Round

`Public Shared Function Round(amount As Currency, digits As Integer = 2, mode As MoneyRoundingMode = MoneyRoundingMode.HalfEven) As Currency`

#### Parameters

| Name | Type | Passing | Default |
| --- | --- | --- | --- |
| `amount` | `Currency` | `ByVal` | Required |
| `digits` | `Integer` | `ByVal` | `2` |
| `mode` | `MoneyRoundingMode` | `ByVal` | `MoneyRoundingMode.HalfEven` |

#### Returns

| Type |
| --- |
| `Currency` |

### Format

`Public Shared Function Format(amount As Currency, digits As Integer = 2, mode As MoneyRoundingMode = MoneyRoundingMode.HalfEven) As String`

Plain decimal text with exactly digits fractional places, rounded first.

#### Parameters

| Name | Type | Passing | Default |
| --- | --- | --- | --- |
| `amount` | `Currency` | `ByVal` | Required |
| `digits` | `Integer` | `ByVal` | `2` |
| `mode` | `MoneyRoundingMode` | `ByVal` | `MoneyRoundingMode.HalfEven` |

#### Returns

| Type |
| --- |
| `String` |

### Allocate

`Public Shared Function Allocate(total As Currency, weights As Array Of Integer, digits As Integer = 4) As Array Of Currency`

Snapshot weights; largest remainder, stable input-order ties; total must already be representable at digits precision. Raw-unit precision is 4.

#### Parameters

| Name | Type | Passing | Default |
| --- | --- | --- | --- |
| `total` | `Currency` | `ByVal` | Required |
| `weights` | `Array Of Integer` | `ByVal` | Required |
| `digits` | `Integer` | `ByVal` | `4` |

#### Returns

| Type |
| --- |
| `Array Of Currency` |
