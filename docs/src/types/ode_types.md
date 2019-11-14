# ODE Problems

## Mathematical Specification of an ODE Problem

To define an ODE Problem, you simply need to give the function ``f`` and the initial
condition ``u₀`` which define an ODE:

```math
\frac{du}{dt} = f(u,p,t)
```

`f` should be specified as `f(u,p,t)` (or in-place as `f(du,u,p,t)`), and `u₀` should
be an AbstractArray (or number) whose geometry matches the desired geometry of `u`.
Note that we are not limited to numbers or vectors for `u₀`; one is allowed to
provide `u₀` as arbitrary matrices / higher dimension tensors as well.

## Problem Type

### Constructors

- `ODEProblem(f::ODEFunction,u0,tspan,p=NullParameters();kwargs...)`
- `ODEProblem{isinplace}(f,u0,tspan,p=NullParameters();kwargs...)` :
  Defines the ODE with the specified functions. `isinplace` optionally sets whether
  the function is inplace or not. This is determined automatically, but not inferred.

Parameters are optional, and if not given then a `NullParameters()` singleton
will be used which will throw nice errors if you try to index non-existent
parameters. Any extra keyword arguments are passed on to the solvers. For example,
if you set a `callback` in the problem, then that `callback` will be added in
every solve call.

For specifying Jacobians and mass matrices, see the
[DiffEqFunctions](http://docs.juliadiffeq.org/latest/features/performance_overloads)
page.

### Fields

* `f`: The function in the ODE.
* `u0`: The initial condition.
* `tspan`: The timespan for the problem.
* `p`: The parameters.
* `kwargs`: The keyword arguments passed onto the solves.

## Example Problems

Example problems can be found in [DiffEqProblemLibrary.jl](https://github.com/JuliaDiffEq/DiffEqProblemLibrary.jl/tree/master/src/ode).

To use a sample problem, such as `prob_ode_linear`, you can do something like:

```julia
#] add DiffEqProblemLibrary
using DiffEqProblemLibrary.ODEProblemLibrary
# load problems
ODEProblemLibrary.importodeproblems()
prob = ODEProblemLibrary.prob_ode_linear
sol = solve(prob)
```

```@docs
DiffEqProblemLibrary.ODEProblemLibrary.prob_ode_linear
DiffEqProblemLibrary.ODEProblemLibrary.prob_ode_2Dlinear
DiffEqProblemLibrary.ODEProblemLibrary.prob_ode_bigfloatlinear
DiffEqProblemLibrary.ODEProblemLibrary.prob_ode_bigfloat2Dlinear
DiffEqProblemLibrary.ODEProblemLibrary.prob_ode_large2Dlinear
DiffEqProblemLibrary.ODEProblemLibrary.prob_ode_2Dlinear_notinplace
DiffEqProblemLibrary.ODEProblemLibrary.prob_ode_lotkavoltera
DiffEqProblemLibrary.ODEProblemLibrary.prob_ode_fitzhughnagumo
DiffEqProblemLibrary.ODEProblemLibrary.prob_ode_threebody
DiffEqProblemLibrary.ODEProblemLibrary.prob_ode_pleides
DiffEqProblemLibrary.ODEProblemLibrary.prob_ode_vanderpol
DiffEqProblemLibrary.ODEProblemLibrary.prob_ode_vanstiff
DiffEqProblemLibrary.ODEProblemLibrary.prob_ode_rober
DiffEqProblemLibrary.ODEProblemLibrary.prob_ode_rigidbody
DiffEqProblemLibrary.ODEProblemLibrary.prob_ode_hires
DiffEqProblemLibrary.ODEProblemLibrary.prob_ode_orego
DiffEqProblemLibrary.ODEProblemLibrary.prob_ode_pollution
DiffEqProblemLibrary.ODEProblemLibrary.prob_ode_nonlinchem
DiffEqProblemLibrary.ODEProblemLibrary.prob_ode_brusselator_1d
DiffEqProblemLibrary.ODEProblemLibrary.prob_ode_brusselator_2d
DiffEqProblemLibrary.ODEProblemLibrary.prob_ode_filament
```
