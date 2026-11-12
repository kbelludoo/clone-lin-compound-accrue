# clone-lin-compound-accrue

Experimental LIN clone of Compound v2 `CToken.accrueInterest` (i64-positive scale, 128-bit floor `(a*b)/1e18`, fail-closed if the quotient does not fit uint64 or `borrowRate > 0.0005e16`).

- **Upstream:** [compound-finance/compound-protocol](https://github.com/compound-finance/compound-protocol) `contracts/CToken.sol` commit `a3214f67b73310d547e00fc578e8355911c9d376` (BSD-3-Clause). This repository does **not** vendor the Solidity source. Hashes only: CToken.sol sha256 `b64790f41ef851b09856af286ce8253b95ef34fda4ae836f924a519e8f792785`, git blob `b8c878c79c75855808f6e7303099a367c8bad98b`. Also pinned: `CTokenInterfaces.sol` (`0.0005e16`) and `ExponentialNoError.sol` (`mul_ScalarTruncate`).
- **LIN kernel:** [`src/lin_compound_accrue.lin`](src/lin_compound_accrue.lin) (sha256 `ecb530de37f6ee4d55e53d3a88322b12c7895e2970f2e69c521af53c888de770`, identical to lin-open)
- **C11 oracle copy:** [`test/oracles/compound_accrue_c11.c`](test/oracles/compound_accrue_c11.c)
- **Proofs (lin-open only):** [kbelludoo/lin-open](https://github.com/kbelludoo/lin-open) `examples/compound_accrue/` and `python3 test/prove_compound_accrue_external.py` (22 PASS / 0 FAIL / 1 SKIP JIT this run)
- **Class:** EXPERIMENTAL. Not Ethereum mainnet uint256. Not a production cToken replacement.

Named goldens (`borrows=1e18`, `rate=1e10`, `index=1e18`): dt=1 interest **10000000000**, borrows/index **1000000010000000000**; `rf=1e17` reserves addend **1000000000**; dt=0 identity; `rate > 0.0005e16` fail-closed **0**; naive i64 `7e18*3e18` wraps to **-5389669316318724096**.
