# Standalone MoneyKit example

Copy main.bui into an empty directory. Create packages/ there and copy
packages/moneykit-0.1.0.buipkg from the repository into it. Run:

    buoy main.bui --check --diagnostic-format json
    buoy main.bui -o money-example
    ./money-example

Expected lines: 33.34, 33.33, 33.33, 7.00. Allocation explicitly uses digits 2;
rate results have native four-place Currency precision until formatted.

Maintainers run the private validation suite before release. See the repository README for public build instructions.
