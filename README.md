# ulam-primes

Finds every prime up to a limit with several algorithms, checks that they all agree, times each one, and draws the result as an Ulam spiral: the whole numbers laid out in a square spiral from the centre, with the primes lit up.

Written in C11 with no dependencies beyond the C standard library.

> **Status: planned, not implemented.** This repository holds the plan only. Every section describes what the first release must do and the bar it must meet.

## Planned algorithms

| Algorithm | Notes |
|---|---|
| Trial division, naive | Baseline |
| Trial division, odd divisors up to the square root | First real improvement |
| Sieve of Eratosthenes | Plain version |
| Sieve of Eratosthenes, odd-only and bit-packed | One bit per odd number |
| Sieve of Eratosthenes, segmented | Works block by block so each block fits in the processor cache |
| Sieve of Sundaram | Different approach, same answer |
| Linear sieve (Euler's sieve) | Marks each composite exactly once |
| Sieve of Atkin | Asymptotically faster, often slower in practice; the benchmark will show where |
| Deterministic Miller–Rabin for 64-bit numbers | Primality test rather than a sieve. Needs a 128-bit multiply-mod, written by hand or with a stated compiler extension |

## Planned output

- **Image files:** PGM or PPM, the plain netpbm formats, written by hand. Every common image viewer opens them.
- **Terminal view:** the spiral drawn with half-block characters and 24-bit colour.
- **Highlights:** colour options for prime-rich polynomials such as Euler's n² + n + 41.
- **Benchmark table and CSV:** time and memory per algorithm and limit.

## Quality bar for the first release

- **Cross-checks:** in `make test`, every algorithm agrees with every other, and with the known prime counts:

  | Limit | Primes below it |
  |---|---|
  | 10⁶ | 78,498 |
  | 10⁷ | 664,579 |
  | 10⁸ | 5,761,455 |
  | 10⁹ | 50,847,534 |

- **Honest timing:** medians of repeated runs, with warm-up, and the compiler, flags and machine stated next to every number.
- **A chart** of time and memory against the limit for each algorithm, with a short explanation of the results, including why the segmented sieve wins.
- **A reference comparison** against [primesieve](https://github.com/kimwalisch/primesieve), to show how far a carefully optimised library goes.
- **Safe builds:** strict compiler warnings, plus the memory and undefined-behaviour checkers on test builds.
- **A one-command build:** `make` builds it and `make test` runs the checks.

## Planned milestones

1. Makefile, strict warnings, the test runner, and the known prime counts.
2. Trial division and the plain sieve, cross-checked.
3. Image output and the first spiral.
4. Timing harness with repeated runs and medians.
5. Odd-only bit-packed sieve and segmented sieve.
6. Sundaram, linear and Atkin sieves; Miller–Rabin.
7. Terminal view, charts and a results write-up.

## Related work

- [PlummersSoftwareLLC/Primes](https://github.com/PlummersSoftwareLLC/Primes): a community prime-sieve "drag race" across languages, and a good guide to fair timing.

## Licence

MIT
