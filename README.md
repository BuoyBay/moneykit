# Compute exact currency amounts, rates and allocations

`Import moneykit` from the sealed `moneykit-0.1.0.buipkg` in a consumer's
`packages/` directory. No dependencies or FFI. All public methods are Shared
methods on `Money`; amounts and results are native `Currency` values.

`MoneyRoundingMode` is a separate enum: `HalfEven`, `HalfAway` (ties away
from zero), `TowardZero`, `Floor`, `Ceiling`. Invalid modes/digits, empty or
nonpositive weights, and a misaligned allocation total throw
`InvalidArgumentException`. Weight-sum or rounded-result overflow throws
`OverflowException`; zero rate denominator throws `DivideByZeroException`.
All numeric inputs accept the full signed Int64 domain, including minimum,
subject to these explicit result and weight bounds.

## Install

From a Buoy consumer project with BPM installed:

```sh
bpm add moneykit --git https://github.com/BuoyBay/moneykit.git --rev refs/heads/main
```

BPM records the resolved commit in its lockfile. Keep that lockfile with the
consumer project for reproducible installs.

## Example

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

## Build from source

With the native `build-packages` driver from [devtools](https://github.com/BuoyBay/devtools)
on your `PATH`, run from this checkout:

```sh
build-packages --root "$PWD" --compile-consumer moneykit
```

The driver checks source targets and compiles an import consumer. See the
[API guide](docs/API.md) for behavior, limits and any host prerequisites.

## Local Buoy setup

On your own machine, install Buoy and run:

```sh
buoy ai init --both
```

The generated agent files and editor settings stay local and are ignored by Git.

## Contributing

[Contributing](CONTRIBUTING.md) · [License](LICENSE)
