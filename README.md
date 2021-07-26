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

julia> @btime (v1+v2).mass
  172.854 ns (4 allocations: 96 bytes)
92.55651f0

julia> @btime fast_mass(v1,v2) # faster function if you only care about mass
  51.800 ns (1 allocation: 16 bytes)
92.55651f0

```
