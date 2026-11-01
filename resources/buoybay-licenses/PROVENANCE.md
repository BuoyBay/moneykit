# Provenance

Original implementation for this workspace; no third-party code copied.
Currency representation and raw conversion contracts were read from installed
Buoy 0.72.0 documentation at /usr/share/buoy/docs/documentation/currency.md.
Integer limb multiplication and binary long division are standard algorithms;
negative-magnitude remainder handling is implemented locally. Tests independently
use Python integers and fractions.Fraction, with seeded random and boundary data.
No upstream mathematical or monetary compliance claims are inherited.
