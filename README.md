# Digital Logic in Oz and Haskell

Implementation of digital logic gates and arithmetic circuits in **Oz** and **Haskell**, used to compare two declarative programming models: concurrent dataflow and lazy evaluation.

The project was inspired by the treatment of digital circuits in *Concepts, Techniques, and Models of Computer Programming*.

## Implemented gates

- NOT
- AND
- OR
- XOR
- NAND

## Implemented circuits

- Half Adder
- Full Adder
- Half Subtractor
- Full Subtractor

## Why two languages?

Both implementations model signals as sequences of bits, but evaluate them differently.

### Oz

The Oz version uses:

- functors for modularization;
- dataflow variables;
- lightweight threads;
- streams represented as lists.

Each gate consumes one or more input streams and produces an output stream.

### Haskell

The Haskell version uses:

- pure functions;
- lazy lists;
- `map` and `zipWith`;
- composition of gates into larger circuits.

Because lists are lazy, the same definitions can also work with streams whose values are produced incrementally.

## Structure

```text
.
├── Haskell/
│   ├── Gates.hs
│   ├── Circuits.hs
│   └── Main.hs
└── Oz/
    ├── Gates.oz
    ├── Circuits.oz
    └── Main.oz
```

## Running the Haskell version

With GHC installed:

```bash
cd Haskell
ghc Main.hs
./Main
```

You can also run it without keeping the compiled executable:

```bash
runghc Main.hs
```

## Running the Oz version

With Mozart/Oz installed:

```bash
cd Oz
ozc -c Gates.oz
ozc -c Circuits.oz
ozc -c Main.oz
ozengine Main.ozf
```

The generated `.ozf` files are build artifacts and are intentionally not versioned.

## Example inputs

The Haskell program evaluates the following streams:

```text
X   = [0, 1, 0, 1]
Y   = [0, 0, 1, 1]
Cin = [0, 0, 0, 0]
Bin = [0, 0, 0, 0]
```

It then prints the output streams for the four arithmetic circuits.

## Learning goals

This project focuses on:

- declarative programming;
- dataflow concurrency;
- lazy evaluation;
- functional decomposition;
- reusable abstractions;
- modeling hardware-like behavior with streams.
