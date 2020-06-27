# Multipoles

Implemenation of the CoMet algorithm from *Mining Novel Multivariate Relationships in Time Series Data Using Correlation Networks*[1] 

For a given set of timeseries, a **multipole** is defined as a subset of two or more timeseries whose dependence and gain are not less than the corresponding thresholds. 
- **Dependence** of a set of timeseries is defined as the variance of the best linear combination and could be computed by 1 minus the least eigenvalue of the correlation matrix of this set. 
- **Gain** of a set of timeseries is defined as the least contribution of each timeseries to the dependence of this set and could be computed by the dependence of this set minus the maximum dependence of subsets generated by removing each timeseries from the set.

## Requirements
Julia 1.0 [2]

Packages:
- Combinatorics
- LightGraphs
- LinearAlgebra

## How to run

In serial:
  ```julia
  julia>include("COMETserial.jl")
  julia>COMETserial(corMat, delta, sigma)
  ```

In parallel
  ```julia 
  julia>include("COMETparallel.jl")
  julia>COMETparallel(corMat, delta, sigma)
  ```

Input:
  - corMat: correlation matrix as a 2D array
  - delta: the dependent threshold
  - sigma: the gain threshold

Return:
  - Vector of multipoles of the following data structure
    ```julia
    struct poles_t{F<:AbstractFloat,I<:Signed}
        dept::F # dependence
        gain::F # gain
        mem::Vector{I}  # indices of member timeseries
    end
    ```

## References
[1] Agrawal, S., Steinbach, M., Boley, D., Chatterjee, S., Atluri, G., Dang, A. T., ... & Kumar, V. (2019). Mining Novel Multivariate Relationships in Time Series Data Using Correlation Networks. IEEE Transactions on Knowledge and Data Engineering.

[2] Julia Download: https://julialang.org/downloads/oldreleases/
