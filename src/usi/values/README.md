# Value types

USI needs to exchange data between the [Host](usi/host.md) and the [Tool](usi/tool.md).
Namely, upon calling the tool, the host will send a bunch of inputs.
After finishing, the tool will return an output.
To facilitate the unification of USI tools, this exchange is done via a canonical list of types, which carry a semantic meaning.


## Bool

Can be `true` or `false`.
Useful for tool flags (e.g.: `use_gpu`)


## Int

64bit signed integer.
Useful for whole-valued settings (e.g.: number of isochromat in a simulation)

Ranges from \\(-2^{63}\\) to \\(2^{63} - 1\\).


## Float

Double-precision IEEE 754 floating point value.
Useful for passing thresholds to the tool or evaluated metrics to the host.

Gives roughly 15 to 17 significant decimal digits: [Wikipedia](https://en.wikipedia.org/wiki/Double-precision_floating-point_format)


## Signal

List of per-coil signals.
For every coil: List of complex ADC sample values.
Each complex value consists of two [Float](#float)'s (real and imaginary value).

Example: a measurement of a 64x64 sequence on a 8-channel system will return a list of 8 lists, each of which contains 4096 complex values.
A single-coil mesurement would return a list containing one element: a list with 4096 samples.


## Encoding

List of `[x, y, z, t]` elements: 4 [Float](#float)'s per ADC sample that store their kt - encoding.

`xyz` represents the \\(\vec{k}\\) dephasing of the measured samples (unit: \\(1 / m\\)). \
`t` is the \\(\tau\\) dephasing: effect of \\(B_0\\) inhomogeneities and \\(T'_2\\) (unit: \\(s\\)).


## VoxelPhantom


## InstantEventSeq