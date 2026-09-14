# X86MacBrew Intel Formula Catalogue

This branch is part of **x86MacBrew**, an independent community project that
continues Homebrew-compatible developer tooling for Intel Macs. It is not
maintained by, endorsed by or an official release of Homebrew.

The repository is an upstream-derived catalogue baseline. Its presence does not
mean that every formula in Homebrew/core is supported on Intel macOS. A formula
becomes an x86MacBrew-supported package only after it meets the project’s Intel
build, test and release requirements.

## Current baseline

| Item | Value |
| --- | --- |
| x86MacBrew core baseline | `baseline/core-intel-macos15-2026-09-11` |
| Upstream base | `Homebrew/homebrew-core` commit `7fd7d31` |
| Initial Intel target | Intel `x86_64` on macOS 15.7.7 |
| Client line | `x86MacBrew/brew` branch `x86macbrew-intel-2027` |

The stable x86MacBrew distribution tap publishes `x86macbrew-doctor` plus the
source-build-tier formulas `oniguruma` and `jq`. Those formulas are not bottles
or core-catalogue guarantees. The active unshipped candidate is `git` on the
tap’s `candidates/git` branch.

## Branch roles

| Branch | Role |
| --- | --- |
| `main` | Reviewed upstream-tracking branch. |
| `x86macbrew-intel-2027` | Maintained Intel catalogue line after the baseline and formula gates are reviewed. |
| `baseline/core-*` | Candidate upstream snapshot with its Intel validation record. |

Do not make this fork the default `HOMEBREW_CORE_GIT_REMOTE` for users until a
reviewed Intel catalogue line exists and at least one formula has completed the
full promotion pipeline.

## Formula promotion requirements

Before a core formula is presented as supported, maintainers must record:

1. an Intel source build from the reviewed formula revision;
2. successful `brew test` and strict audit results;
3. a meaningful runtime smoke test;
4. an independent clean Intel host or clean Intel macOS volume installation;
5. bottle checksum, build provenance and clean-host bottle test if a bottle is
   published; and
6. a reviewed release-manifest entry in the x86MacBrew distribution tap.

The project may retain experimental source-build candidates separately, but it
must not represent them as stable catalogue support.

## Upstream synchronization

For every upstream update:

1. fetch and review the new `Homebrew/homebrew-core` revision;
2. create an `x86macbrew-intel-2027` candidate branch instead of publishing a
   blind fast-forward;
3. run the Intel client and selected-formula validation matrix;
4. record failures, compatibility patches and skipped components; and
5. merge only the reviewed result through a pull request.

Security fixes should be prioritized, but they still require an Intel runtime
check before release. Intel-only compatibility changes should remain small,
documented and attributable to the upstream change that made them necessary.

## Scope boundary

x86MacBrew does not promise all Homebrew formulae, upstream bottle parity or
cask parity. Closed-source software that vendors ship only for Apple Silicon
cannot become an Intel package merely by being listed in a catalogue fork.
