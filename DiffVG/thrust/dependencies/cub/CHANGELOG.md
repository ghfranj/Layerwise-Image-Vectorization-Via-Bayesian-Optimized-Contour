# CUB 1.9.10-1 (NVIDIA HPC SDK 20.7, CUDA Toolkit 11.1)

## Summary

CUB 1.9.10-1 is the minor release accompanying the NVIDIA HPC SDK 20.7 release
  and the CUDA Toolkit 11.1 release.

## Bug Fixes

- #1217: Move static local in `cub::DeviceCount` to a separate host-only
    function because NVC++ doesn't support static locals in host-device
    functions.

# CUB 1.9.10 (NVIDIA HPC SDK 20.5)

## Summary

Thrust 1.9.10 is the release accompanying the NVIDIA HPC SDK 20.5 release.
It adds CMake `find_package` support.
C++03, C++11, GCC < 5, Clang < 6, and MSVC < 2017 are now deprecated.
Starting with the upcoming 1.10.0 release, C++03 support will be dropped
  entirely.

## Breaking Changes

- Thrust now checks that it is compatible with the version of CUB found
    in your include path, generating an error if it is not.
  If you are using your own version of CUB, it may be too old.
  It is recommended to simply delete your own version of CUB and use the
    version of CUB that comes with Thrust.
- C++03 and C++11 are deprecated.
  Using these dialects will generate a compile-time warning.
  These warnings can be suppressed by defining
    `CUB_IGNORE_DEPRECATED_CPP_DIALECT` (to suppress C++03 and C++11
    deprecation warnings) or `CUB_IGNORE_DEPRECATED_CPP_11` (to suppress C++11
    deprecation warnings).
  Suppression is only a short term solution.
  We will be dropping support for C++03 in the 1.10.0 release and C++11 in the
    near future.
- GCC < 5, Clang < 6, and MSVC < 2017 are deprecated.
  Using these compilers will generate a compile-time warning.
  These warnings can be suppressed by defining
  `CUB_IGNORE_DEPRECATED_COMPILER`.
  Suppression is only a short term solution.
  We will be dropping support for these compilers in the near future.

## New Features

- CMake `find_package` support.
  Just point CMake at the `cmake` folder in your CUB include directory
    (ex: `cmake -DCUB_DIR=/usr/local/cuda/include/cub/cmake/ .`) and then you
    can add CUB to your CMake project with `find_package(CUB REQUIRED CONFIG)`.

# CUB 1.9.9 (CUDA 11.0)

## Summary

CUB 1.9.9 is the release accompanying the CUDA Toolkit 11.0 release.
It introduces CMake support, version macros, platform detection machinery,
  and support for NVC++, which uses Thrust (and thus CUB) to implement
  GPU-accelerated C++17 Parallel Algorithms.
Additionally, the scan dispatch layer was refactored and modernized.
C++03, C++11, GCC < 5, Clang < 6, and MSVC < 2017 are now deprecated.
Starting with the upcoming 1.10.0 release, C++03 support will be dropped
  entirely.

## Breaking Changes

- Thrust now checks that it is compatible with the version of CUB found
    in your include path, generating an error if it is not.
  If you are using your own version of CUB, it may be too old.
  It is recommended to simply delete your own version of CUB and use the
    version of CUB that comes with Thrust.
- C++03 and C++11 are deprecated.
  Using these dialects will generate a compile-time warning.
  These warnings can be suppressed by defining
    `CUB_IGNORE_DEPRECATED_CPP_DIALECT` (to suppress C++03 and C++11
    deprecation warnings) or `CUB_IGNORE_DEPRECATED_CPP11` (to suppress C++11
    deprecation warnings).
  Suppression is only a short term solution.
  We will be dropping support for C++03 in the 1.10.0 release and C++11 in the
    near future.
- GCC < 5, Clang < 6, and MSVC < 2017 are deprecated.
  Using these compilers will generate a compile-time warning.
  These warnings can be suppressed by defining
    `CUB_IGNORE_DEPRECATED_COMPILER`.
  Suppression is only a short term solution.
  We will be dropping support for these compilers in the near future.

## New Features

- CMake support.
  Thanks to Francis Lemaire for this contribution.
- Refactorized and modernized scan dispatch layer.
  Thanks to Francis Lemaire for this contribution.
- Policy hooks for device-wide reduce, scan, and radix sort facilities
    to simplify tuning and allow users to provide custom policies.
  Thanks to Francis Lemaire for this contribution.
- `<cub/version.cuh>`: `CUB_VERSION`, `CUB_VERSION_MAJOR`, `CUB_VERSION_MINOR`,
    `CUB_VERSION_SUBMINOR`, and `CUB_PATCH_NUMBER`.
- Platform detection machinery:
  - `<cub/util_cpp_dialect.cuh>`: Detects the C++ standard dialect.
  - `<cub/util_compiler.cuh>`: host and device compiler detection.
  - `<cub/util_deprecated.cuh>`: `CUB_DEPRECATED`.
  - <cub/config.cuh>`: Includes `<cub/util_arch.cuh>`,
      `<cub/util_compiler.cuh>`, `<cub/util_cpp_dialect.cuh>`,
      `<cub/util_deprecated.cuh>`, `<cub/util_macro.cuh>`,
      `<cub/util_namespace.cuh>`
- `cub::DeviceCount` and `cub::DeviceCountUncached`, caching abstractions for
    `cudaGetDeviceCount`.

## Other Enhancements

- Lazily initialize the per-device CUDAattribute caches, because CUDA context
    creation is expensive and adds up with large CUDA binaries on machines with
    many GPUs.
  Thanks to the NVIDIA PyTorch team for bringing this to our attention.
- Make `cub::SwitchDevice` avoid setting/resetting the device if the current
    device is the same as the target device.

## Bug Fixes

- Add explicit failure parameter to CAS in the CUB attribute cache to workaround
    a GCC 4.8 bug.
- Revert a change in reductions that changed the signedness of the `lane_id`
    variable to suppress a warning, as this introduces a bug in optimized device
    code.
- Fix initialization in `cub::ExclusiveSum`.
  Thanks to Conor Hoekstra for this contribution.
- Fix initialization of the `std::array` in the CUB attribute cache.
- Fix `-Wsign-compare` warnings.
  Thanks to Elias Stehle for this contribution.
- Fix `test_block_reduce.cu` to build without parameters.
  Thanks to Francis Lemaire for this contribution.
- Add missing includes to `grid_even_share.cuh`.
  Thanks to Francis Lemaire for this contribution.
- Add missing includes to `thread_search.cuh`.
  Thanks to Francis Lemaire for this contribution.
- Add missing includes to `cub.cuh`.
  Thanks to Felix Kallenborn for this contribution.

# CUB 1.9.8-1 (NVIDIA HPC SDK 20.3)

## Summary

CUB 1.9.8-1 is a variant of 1.9.8 accompanying the NVIDIA HPC SDK 20.3 release.
It contains modifications necessary to serve as the implementation of NVC++'s
  GPU-accelerated C++17 Parallel Algorithms.

# CUB 1.9.8 (CUDA 11.0 Early Access)

## Summary

CUB 1.9.8 is the first release of CUB to be officially supported and included
  in the CUDA Toolkit.
When compiling CUB in C++11 mode, CUB now caches calls to CUDA attribute query
  APIs, which improves performance of these queries by 20x to 50x when they
  are called concurrently by multiple host threads.

## Enhancements

- (C++11 or later) Cache calls to `cudaFuncGetAttributes` and
    `cudaDeviceGetAttribute` within `cub::PtxVersion` and `cub::SmVersion`.
    These CUDA APIs acquire locks to CUDA driver/runtime mutex and perform
    poorly under contention; with the caching, they are 20 to 50x faster when
    called concurrently.
  Thanks to Bilge Acun for bringing this issue to our attention.
- `DispatchReduce` now takes an `OutputT` template parameter so that users can
    specify the intermediate type explicitly.
- Radix sort tuning policies updates to fix performance issues for element
    types smaller than 4 bytes.

## Bug Fixes

- Change initialization style from copy initialization to direct initialization
    (which is more permissive) in `AgentReduce` to allow a wider range of types
    to be used with it.
- Fix bad signed/unsigned comparisons in `WarpReduce`.
- Fix computation of valid lanes in warp-level reduction primitive to correctly
    handle the case where there are 0 input items per warp.

# CUB 1.8.0

## Summary

CUB 1.8.0 introduces changes to the `cub::Shuffle*` interfaces.

## Breaking Changes

- The interfaces of `cub::ShuffleIndex`, `cub::ShuffleUp`, and
    `cub::ShuffleDown` have been changed to allow for better computation of the
    PTX SHFL control constant for logical warps smaller than 32 threads.

## Bug Fixes

- #112: Fix `cub::WarpScan`'s broadcast of warp-wide aggregate for logical
    warps smaller than 32 threads.

# CUB 1.7.5

## Summary

CUB 1.7.5 adds support for radix sorting `__half` keys and improved sorting
  performance for 1 byte keys.
It was incorporated into Thrust 1.9.2.

## Enhancements

- Radix sort support for `__half` keys.
- Radix sort tuning policy updates to improve 1 byte key performance.

## Bug Fixes

- Syntax tweaks to mollify Clang.
- #127: `cub::DeviceRunLengthEncode::Encode` returns incorrect results.
- #128: 7-bit sorting passes fail for SM61 with large values.

# CUB 1.7.4

## Summary

CUB 1.7.4 is a minor release that was incorporated into Thrust 1.9.1-2.

## Bug Fixes

- #114: Can't pair non-trivially-constructible values in radix sort.
- #115: `cub::WarpReduce` segmented reduction is broken in CUDA 9 for logical
    warp sizes smaller than 32.

# CUB 1.7.3

## Summary

CUB 1.7.3 is a minor release.

## Bug Fixes

- #110: `cub::DeviceHistogram` null-pointer exception bug for iterator inputs.

# CUB 1.7.2

## Summary

CUB 1.7.2 is a minor release.

## Bug Fixes

- #104: Device-wide reduction is now "run-to-run" deterministic for
    pseudo-associative reduction operators (like floating point addition).

# CUB 1.7.1

## Summary

CUB 1.7.1 delivers improved radix sort performance on SM7x (Volta) GPUs and a
  number of bug fixes.

## Enhancements

- Radix sort tuning policies updated for SM7x (Volta).

## Bug Fixes

- #104: `uint64_t` `cub::WarpReduce` broken for CUB 1.7.0 on CUDA 8 and older.
- #103: Can't mix Thrust from CUDA 9.0 and CUB.
- #102: CUB pulls in `windows.h` which defines `min`/`max` macros that conflict
    with `std::min`/`std::max`.
- #99: Radix sorting crashes NVCC on Windows 10 for SM52.
- #98: cuda-memcheck: --tool initcheck failed with lineOfSight.
- #94: Git clone size.
- #93: Accept iterators for segment offsets.
- #87: CUB uses anonymous unions which is not valid C++.
- #44: Check for C++11 is incorrect for Visual Studio 2013.

# CUB 1.7.0

## Summary

CUB 1.7.0 brings support for CUDA 9.0 and SM7x (Volta) GPUs.
It is compatible with independent thread scheduling.
It was incorporated into Thrust 1.9.0-5.

## Breaking Changes

- Remove `cub::WarpAll` and `cub::WarpAny`.
  These functions served to emulate `__all` and `__any` functionality for
    SM1x devices, which did not have those operations.
  However, SM1x devices are now deprecated in CUDA, and the interfaces of these
    two functions are now lacking the lane-mask needed for collectives to run on
    SM7x and newer GPUs which have independent thread scheduling.

## Other Enhancements

- Remove any assumptions of implicit warp synchronization to be compatible with
    SM7x's (Volta) independent thread scheduling.

## Bug Fixes

- #86: Incorrect results with reduce-by-key.

# CUB 1.6.4

## Summary

CUB 1.6.4 improves radix sorting performance for SM5x (Maxwell) and SM6x
  (Pascal) GPUs.

## Enhancements

- Radix sort tuning policies updated for SM5x (Maxwell) and SM6x (Pascal) -
    3.5B and 3.4B 32 byte keys/s on TitanX and GTX 1080, respectively.

## Bug Fixes

- Restore fence work-around for scan (reduce-by-key, etc.) hangs in CUDA 8.5.
- #65: `cub::DeviceSegmentedRadixSort` should allow inputs to have
    pointer-to-const type.
- Mollify Clang device-side warnings.
- Remove out-dated MSVC project files.

# CUB 1.6.3

## Summary

CUB 1.6.3 improves support for Windows, changes
  `cub::BlockLoad`/`cub::BlockStore` interface to take the local data type,
  and enhances radix sort performance for SM6x (Pascal) GPUs.

## Breaking Changes

- `cub::BlockLoad` and `cub::BlockStore` are now templated by the local data
    type, instead of the `Iterator` type.
  This allows for output iterators having `void` as their `value_type` (e.g.
    discard iterators).

## Other Enhancements

- Radix sort tuning policies updated for SM6x (Pascal) GPUs - 6.2B 4 byte
    keys/s on GP100.
- Improved support for Windows (warnings, alignment, etc).

## Bug Fixes

- #74: `cub::WarpReduce` executes reduction operator for out-of-bounds items.
- #72: `cub:InequalityWrapper::operator` should be non-const.
- #71: `cub::KeyValuePair` won't work if `Key` has non-trivial constructor.
- #69: cub::BlockStore::Store` doesn't compile if `OutputIteratorT::value_type`
    isn't `T`.
- #68: `cub::TilePrefixCallbackOp::WarpReduce` doesn't permit PTX arch
    specialization.

# CUB 1.6.2 (previously 1.5.5)

## Summary

CUB 1.6.2 (previously 1.5.5) improves radix sort performance for SM6x (Pascal)
  GPUs.

## Enhancements

- Radix sort tuning policies updated for SM6x (Pascal) GPUs.

## Bug Fixes

- Fix AArch64 compilation of `cub::CachingDeviceAllocator`.

# CUB 1.6.1 (previously 1.5.4)

## Summary

CUB 1.6.1 (previously 1.5.4) is a minor release.

## Bug Fixes

- Fix radix sorting bug introduced by scan refactorization.

# CUB 1.6.0 (previously 1.5.3)

## Summary

CUB 1.6.0 changes the scan and reduce interfaces.
Exclusive scans now accept an "initial value" instead of an "identity value".
Scans and reductions now support differing input and output sequence types.
Additionally, many bugs have been fixed.

## Breaking Changes

- Device/block/warp-wide exclusive scans have been revised to now accept an
    "initial value" (instead of an "identity value") for seeding the computation
    with an arbitrary prefix.
- Device-wide reductions and scans can now have input sequence types that are
    different from output sequence types (as long as they are convertible).

## Other Enhancements

- Reduce repository size by moving the doxygen binary to doc repository.
- Minor reduction in `cub::BlockScan` instruction counts.

## Bug Fixes

- Issue #55: Warning in `cub/device/dispatch/dispatch_reduce_by_key.cuh`.
- Issue #59: `cub::DeviceScan::ExclusiveSum` can't prefix sum of float into
    double.
- Issue #58: Infinite loop in `cub::CachingDeviceAllocator::NearestPowerOf`.
- Issue #47: `cub::CachingDeviceAllocator` needs to clean up CUDA global error
    state upon successful retry.
- Issue #46: Very high amount of needed memory from the
    `cub::DeviceHistogram::HistogramEven`.
- Issue #45: `cub::CachingDeviceAllocator` fails with debug output enabled

# CUB 1.5.2

## Summary

CUB 1.5.2 enhances `cub::CachingDeviceAllocator` and improves scan performance
  for SM5x (Maxwell).

## Enhancements

- Improved medium-size scan performance on SM5x (Maxwell).
- Refactored `cub::CachingDeviceAllocator`:
  - Now spends less time locked.
  - Uses C++11's `std::mutex` when available.
  - Failure to allocate a block from the runtime will retry once after
  		freeing cached allocations.
  - Now respects max-bin, fixing an issue where blocks in excess of max-bin
      were still being retained in the free cache.

## Bug fixes:

- Fix for generic-type reduce-by-key `cub::WarpScan` for SM3x and newer GPUs.

# CUB 1.5.1

## Summary

CUB 1.5.1 is a minor release.

## Bug Fixes

- Fix for incorrect `cub::DeviceRadixSort` output for some small problems on
    SM52 (Mawell) GPUs.
- Fix for macro redefinition warnings when compiling `thrust::sort`.

# CUB 1.5.0

CUB 1.5.0 introduces segmented sort and reduction primitives.

## New Features:

- Segmented device-wide operations for device-wide sort and reduction primitives.

## Bug Fixes:

- #36: `cub::ThreadLoad` generates compiler errors when loading from
    pointer-to-const.
- #29: `cub::DeviceRadixSort::SortKeys<bool>` yields compiler errors.
- #26: Misaligned address after `cub::DeviceRadixSort::SortKeys`.
- #25: Fix for incorrect results and crashes when radix sorting 0-length
    problems.
- Fix CUDA 7.5 issues on SM52 GPUs with SHFL-based warp-scan and
    warp-reduction on non-primitive data types (e.g. user-defined structs).
- Fix small radix sorting problems where 0 temporary bytes were required and
    users code was invoking `malloc(0)` on some systems where that returns
    `NULL`.
  CUB assumed the user was asking for the size again and not running the sort.

# CUB 1.4.1

## Summary

CUB 1.4.1 is a minor release.

## Enhancements

- Allow `cub::DeviceRadixSort` and `cub::BlockRadixSort` on bool types.

## Bug Fixes

- Fix minor CUDA 7.0 performance regressions in `cub::DeviceScan` and
    `cub::DeviceReduceByKey`.
- Remove requirement for callers to define the `CUB_CDP` macro
    when invoking CUB device-wide rountines using CUDA dynamic parallelism.
- Fix headers not being included in the proper order (or missing includes)
    for some block-wide functions.

# CUB 1.4.0

## Summary

CUB 1.4.0 adds `cub::DeviceSpmv`, `cub::DeviceRunLength::NonTrivialRuns`,
  improves `cub::DeviceHistogram`, and introduces support for SM5x (Maxwell)
  GPUs.

## New Features:

- `cub::DeviceSpmv` methods for multiplying sparse matrices by
    dense vectors, load-balanced using a merge-based parallel decomposition.
- `cub::DeviceRadixSort` sorting entry-points that always return
    the sorted output into the specified buffer, as opposed to the
    `cub::DoubleBuffer` in which it could end up in either buffer.
- `cub::DeviceRunLengthEncode::NonTrivialRuns` for finding the starting
    offsets and lengths of all non-trivial runs (i.e., length > 1) of keys in
    a given sequence.
  Useful for top-down partitioning algorithms like MSD sorting of very-large
    keys.

## Other Enhancements

- Support and performance tuning for SM5x (Maxwell) GPUs.
- Updated cub::DeviceHistogram implementation that provides the same
    "histogram-even" and "histogram-range" functionality as IPP/NPP.
  Provides extremely fast and, perhaps more importantly, very uniform
    performance response across diverse real-world datasets, including
    pathological (homogeneous) sample distributions.

# CUB 1.3.2

## Summary

CUB 1.3.2 is a minor release.

## Bug Fixes

- Fix `cub::DeviceReduce` where reductions of small problems (small enough to
    only dispatch a single thread block) would run in the default stream (stream
    zero) regardless of whether an alternate stream was specified.

# CUB 1.3.1

## Summary

CUB 1.3.1 is a minor release.

## Bug Fixes

- Workaround for a benign WAW race warning reported by cuda-memcheck
    in `cub::BlockScan` specialized for `BLOCK_SCAN_WARP_SCANS` algorithm.
- Fix bug in `cub::DeviceRadixSort` where the algorithm may sort more
    key bits than the caller specified (up to the nearest radix digit).
- Fix for ~3% `cub::DeviceRadixSort` performance regression on SM2x (Fermi) and
    SM3x (Kepler) GPUs.

# CUB 1.3.0

## Summary

CUB 1.3.0 improves how thread blocks are expressed in block- and warp-wide
  primitives and adds an enhanced version of `cub::WarpScan`.

## Breaking Changes

- CUB's collective (block-wide, warp-wide) primitives underwent a minor
    interface refactoring:
  - To provide the appropriate support for multidimensional thread blocks,
      The interfaces for collective classes are now template-parameterized by
      X, Y, and Z block dimensions (with `BLOCK_DIM_Y` and `BLOCK_DIM_Z` being
      optional, and `BLOCK_DIM_X` replacing `BLOCK_THREADS`).
    Furthermore, the constructors that accept remapped linear
      thread-identifiers have been removed: all primitives now assume a
      row-major thread-ranking for multidimensional thread blocks.
  - To allow the host program (compiled by the host-pass) to accurately
      determine the device-specific storage requirements for a given collective
      (compiled for each device-pass), the interfaces for collective classes
      are now (optionally) template-parameterized by the desired PTX compute
      capability.
    This is useful when aliasing collective storage to shared memory that has
      been allocated dynamically by the host at the kernel call site.
  - Most CUB programs having typical 1D usage should not require any
      changes to accomodate these updates.

## New Features

- Added "combination" `cub::WarpScan` methods for efficiently computing
    both inclusive and exclusive prefix scans (and sums).

## Bug Fixes

- Fix for bug in `cub::WarpScan` (which affected `cub::BlockScan` and
    `cub::DeviceScan`) where incorrect results (e.g., NAN) would often be
    returned when parameterized for floating-point types (fp32, fp64).
- Workaround for ptxas error when compiling with with -G flag on Linux (for
    debug instrumentation).
- Fixes for certain scan scenarios using custom scan operators where code
    compiled for SM1x is run on newer GPUs of higher compute-capability: the
    compiler could not tell which memory space was being used collective
    operations and was mistakenly using global ops instead of shared ops.

# CUB 1.2.3

## Summary

CUB 1.2.3 is a minor release.

## Bug Fixes

- Fixed access violation bug in `cub::DeviceReduce::ReduceByKey` for
    non-primitive value types.
- Fixed code-snippet bug in `ArgIndexInputIteratorT` documentation.

# CUB 1.2.2

## Summary

CUB 1.2.2 adds a new variant of `cub::BlockReduce` and MSVC project solections
  for examples.

## New Features

- MSVC project solutions for device-wide and block-wide examples
- New algorithmic variant of cub::BlockReduce for improved performance
    when using commutative operators (e.g., numeric addition).

## Bug Fixes

- Inclusion of Thrust headers in a certain order prevented CUB device-wide
    primitives from working properly.

# CUB 1.2.0

## Summary

CUB 1.2.0 adds `cub::DeviceReduce::ReduceByKey` and
  `cub::DeviceReduce::RunLengthEncode` and support for CUDA 6.0.

## New Features

- `cub::DeviceReduce::ReduceByKey`.
- `cub::DeviceReduce::RunLengthEncode`.

## Other Enhancements

- Improved `cub::DeviceScan`, `cub::DeviceSelect`, `cub::DevicePartition`
    performance.
- Documentation and testing:
  - Added performance-portability plots for many device-wide primitives.
  - Explain that iterator (in)compatibilities with CUDA 5.0 (and older) and
      Thrust 1.6 (and older).
- Revised the operation of temporary tile status bookkeeping for
    `cub::DeviceScan` (and similar) to be safe for current code run on future
    platforms (now uses proper fences).

## Bug Fixes

- Fix `cub::DeviceScan` bug where Windows alignment disagreements between host
    and device regarding user-defined data types would corrupt tile status.
- Fix `cub::BlockScan` bug where certain exclusive scans on custom data types
    for the `BLOCK_SCAN_WARP_SCANS` variant would return incorrect results for
    the first thread in the block.
- Added workaround to make `cub::TexRefInputIteratorT` work with CUDA 6.0.

# CUB 1.1.1

## Summary

CUB 1.1.1 introduces texture and cache modifier iterators, descending sorting,
  `cub::DeviceSelect`, `cub::DevicePartition`, `cub::Shuffle*`, and
  `cub::MaxSMOccupancy`.
Additionally, scan and sort performance for older GPUs has been improved and
  many bugs have been fixed.

## Breaking Changes

- Refactored block-wide I/O (`cub::BlockLoad` and `cub::BlockStore`), removing
    cache-modifiers from their interfaces.
  `cub::CacheModifiedInputIterator` and `cub::CacheModifiedOutputIterator`
    should now be used with `cub::BlockLoad` and `cub::BlockStore` to effect that
    behavior.

## New Features

- `cub::TexObjInputIterator`, `cub::TexRefInputIterator`,
    `cub::CacheModifiedInputIterator`, and `cub::CacheModifiedOutputIterator`
    types for loading & storing arbitrary types through the cache hierarchy.
  They are compatible with Thrust.
- Descending sorting for `cub::DeviceRadixSort` and `cub::BlockRadixSort`.
- Min, max, arg-min, and arg-max operators for `cub::DeviceReduce`.
- `cub::DeviceSelect` (select-unique, select-if, and select-flagged).
- `cub::DevicePartition` (partition-if, partition-flagged).
- Generic `cub::ShuffleUp`, `cub::ShuffleDown`, and `cub::ShuffleIndex` for
    warp-wide communication of arbitrary data types (SM3x and up).
- `cub::MaxSmOccupancy` for accurately determining SM occupancy for any given
    kernel function pointer.

## Other Enhancements

- Improved `cub::DeviceScan` and `cub::DeviceRadixSort` performance for older
    GPUs (SM1x to SM3x).
- Renamed device-wide `stream_synchronous` param to `debug_synchronous` to
    avoid confusion about usage.
- Documentation improvements:
  - Added simple examples of device-wide methods.
  - Improved doxygen documentation and example snippets.
- Improved test coverege to include up to 21,000 kernel variants and 851,000
    unit tests (per architecture, per platform).

## Bug Fixes

- Fix misc `cub::DeviceScan, BlockScan, DeviceReduce, and BlockReduce bugs when
    operating on non-primitive types for older architectures SM1x.
- SHFL-based scans and reductions produced incorrect results for multi-word
    types (size > 4B) on Linux.
- For `cub::WarpScan`-based scans, not all threads in the first warp were
    entering the prefix callback functor.
- `cub::DeviceRadixSort` had a race condition with key-value pairs for pre-SM35
    architectures.
- `cub::DeviceRadixSor` bitfield-extract behavior with long keys on 64-bit
    Linux was incorrect.
- `cub::BlockDiscontinuity` failed to compile for types other than
    `int32_t`/`uint32_t`.
- CUDA Dynamic Parallelism (CDP, e.g. device-callable) versions of device-wide
    methods now report the same temporary storage allocation size requirement as
    their host-callable counterparts.

# CUB 1.0.2

## Summary

CUB 1.0.2 is a minor release.

## Bug Fixes

- Corrections to code snippet examples for `cub::BlockLoad`, `cub::BlockStore`,
    and `cub::BlockDiscontinuity`.
- Cleaned up unnecessary/missing header includes.
  You can now safely include a specific .cuh (instead of `cub.cuh`).
- Bug/compilation fixes for `cub::BlockHistogram`.

# CUB 1.0.1

## Summary

CUB 1.0.1 adds `cub::DeviceRadixSort` and `cub::DeviceScan`.
Numerous other performance and correctness fixes and included.

## Breaking Changes

- New collective interface idiom (specialize/construct/invoke).

## New Features

- `cub::DeviceRadixSort`.
  Implements short-circuiting for homogenous digit passes.
- `cub::DeviceScan`.
  Implements single-pass "adaptive-lookback" strategy.

## Other Enhancements

- Significantly improved documentation (with example code snippets).
- More extensive regression test suit for aggressively testing collective
    variants.
- Allow non-trially-constructed types (previously unions had prevented aliasing
    temporary storage of those types).
- Improved support for SM3x SHFL (collective ops now use SHFL for types larger
    than 32 bits).
- Better code generation for 64-bit addressing within
    `cub::BlockLoad`/`cub::BlockStore`.
- `cub::DeviceHistogram` now supports histograms of arbitrary bins.
- Updates to accommodate CUDA 5.5 dynamic parallelism.

## Bug Fixes

- Workarounds for SM10 codegen issues in uncommonly-used
    `cub::WarpScan`/`cub::WarpReduce` specializations.

# CUB 0.9.4

## Summary

CUB 0.9.3 is a minor release.

## Enhancements

- Various documentation updates and corrections.

## Bug Fixes

- Fixed compilation errors for SM1x.
- Fixed compilation errors for some WarpScan entrypoints on SM3x and up.

# CUB 0.9.3

## Summary

CUB 0.9.3 adds histogram algorithms and work management utility descriptors.

## New Features

- `cub::DevicHistogram256`.
- `cub::BlockHistogram256`.
- `cub::BlockScan` algorithm variant `BLOCK_SCAN_RAKING_MEMOIZE`, which
    trades more register consumption for less shared memory I/O.
- `cub::GridQueue`, `cub::GridEvenShare`, work management utility descriptors.

## Other Enhancements

- Updates to `cub::BlockRadixRank` to use `cub::BlockScan`, which improves
    performance on SM3x by using SHFL.
- Allow types other than builtin types to be used in `cub::WarpScan::*Sum`
    methods if they only have `operator+` overloaded.
  Previously they also required to support assignment from `int(0)`.
- Update `cub::BlockReduce`'s `BLOCK_REDUCE_WARP_REDUCTIONS` algorithm to work
    even when block size is not an even multiple of warp size.
- Refactoring of `cub::DeviceAllocator` interface and
    `cub::CachingDeviceAllocator` implementation.

# CUB 0.9.2

## Summary

CUB 0.9.2 adds `cub::WarpReduce`.

## New Features

- `cub::WarpReduce`, which uses the SHFL instruction when applicable.
  `cub::BlockReduce` now uses this `cub::WarpReduce` instead of implementing
    its own.

## Enhancements

- Documentation updates and corrections.

## Bug Fixes

- Fixes for 64-bit Linux compilation warnings and errors.

# CUB 0.9.1

## Summary

CUB 0.9.1 is a minor release.

## Bug Fixes

- Fix for ambiguity in `cub::BlockScan::Reduce` between generic reduction and
    summation.
  Summation entrypoints are now called `::Sum()`, similar to the
    convention in `cub::BlockScan`.
- Small edits to documentation and download tracking.

# CUB 0.9.0

## Summary

Initial preview release.
CUB is the first durable, high-performance library of cooperative block-level,
  warp-level, and thread-level primitives for CUDA kernel programming.

