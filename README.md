# LVCyl.jl

This package is a minimal version of [LorentzVectors.jl](https://github.com/JLTastet/LorentzVectors.jl) except using
a cylindrical coordinate system (pT, eta, phi, mass) instead of cartesian (t, x, y, z).

The package is currently unregistered.

## Usage

```julia
julia> using LVCyl

julia> v1 = LorentzVectorCyl(43.71242f0, 1.4733887f0, 1.6855469f0, 0.10571289f0)
julia> v2 = LorentzVectorCyl(36.994347f0, 0.38684082f0, -1.3935547f0, 0.10571289f0)

julia> v1+v2
LorentzVectorCyl{Float32}(pt=7.1725554, eta=3.3784156, phi=1.3575952, mass=92.55651)

julia> (v1+v2).mass
92.55651f0
```

If you only care about mass, it's much faster to compute.

```julia
julia> using BenchmarkTools

julia> @btime ($v1+$v2).mass
  85.620 ns (0 allocations: 0 bytes)
92.55651f0

julia> @btime fast_mass($v1,$v2)
  20.447 ns (0 allocations: 0 bytes)
92.55651f0
```

Some other helper functions

```julia
julia> deltaphi(v1,v2)
-3.0791016f0

julia> deltar(v1,v2)
3.265188f0

# convert to cartesian `LorentzVector`...
julia> using LorentzVectors

julia> tocartesian(v1)
(t = 100.38882f0, x = -5.0050235f0, y = 43.424942f0, z = 90.37216f0)

julia> LorentzVector(tocartesian(v1)...) 
LorentzVector{Float32}(100.38882f0, -5.0050235f0, 43.424942f0, 90.37216f0)
```
