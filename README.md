<!---
This file was generated from `meta.yml`, please do not edit manually.
Follow the instructions on https://github.com/coq-community/templates to regenerate.
--->
# CoqEAL

[![Docker CI][docker-action-shield]][docker-action-link]
[![Contributing][contributing-shield]][contributing-link]
[![Code of Conduct][conduct-shield]][conduct-link]
[![Zulip][zulip-shield]][zulip-link]

[docker-action-shield]: https://github.com/coq-community/coqeal/workflows/Docker%20CI/badge.svg?branch=master
[docker-action-link]: https://github.com/coq-community/coqeal/actions?query=workflow:"Docker%20CI"

[contributing-shield]: https://img.shields.io/badge/contributions-welcome-%23f7931e.svg
[contributing-link]: https://github.com/coq-community/manifesto/blob/master/CONTRIBUTING.md

[conduct-shield]: https://img.shields.io/badge/%E2%9D%A4-code%20of%20conduct-%23f15a24.svg
[conduct-link]: https://github.com/coq-community/manifesto/blob/master/CODE_OF_CONDUCT.md

[zulip-shield]: https://img.shields.io/badge/chat-on%20zulip-%23c1272d.svg
[zulip-link]: https://coq.zulipchat.com/#narrow/stream/237663-coq-community-devs.20.26.20users



This Coq library contains a subset of the work that was developed in the context
of the ForMath EU FP7 project (2009-2013). It has two parts:
- theory, which contains developments in algebra and optimized algorithms on mathcomp data structures.
- refinements, which is a framework to ease change of data representations during a proof.

## Meta

- Author(s):
  - Guillaume Cano (initial)
  - Cyril Cohen (initial)
  - Maxime Dénès (initial)
  - Érik Martin-Dorel
  - Anders Mörtberg (initial)
  - Damien Rouhling
  - Pierre Roux
  - Vincent Siles (initial)
- Coq-community maintainer(s):
  - Cyril Cohen ([**@CohenCyril**](https://github.com/CohenCyril))
  - Pierre Roux ([**@proux01**](https://github.com/proux01))
- License: [MIT License](LICENSE)
- Compatible Coq versions: 8.10 or later (use releases for other Coq versions)
- Additional dependencies:
  - [Bignums](https://github.com/coq/bignums) same version as Coq
  - [Paramcoq](https://github.com/coq-community/paramcoq) 1.1.1 or later
  - [MathComp Multinomials](https://github.com/math-comp/multinomials) >= 1.5.1 and < 1.7
  - [MathComp](https://math-comp.github.io) 1.12.0 or newer
- Coq namespace: `CoqEAL`
- Related publication(s):
  - [A refinement-based approach to computational algebra in Coq](https://hal.inria.fr/hal-00734505/document) doi:[10.1007/978-3-642-32347-8_7](https://doi.org/10.1007/978-3-642-32347-8_7)
  - [Refinements for free!](https://hal.inria.fr/hal-01113453/document) doi:[10.1007/978-3-319-03545-1_10](https://doi.org/10.1007/978-3-319-03545-1_10)
  - [A Coq Formalization of Finitely Presented Modules](https://hal.inria.fr/hal-01378905/document) doi:[10.1007/978-3-319-08970-6_13](https://doi.org/10.1007/978-3-319-08970-6_13)
  - [Formalized Linear Algebra over Elementary Divisor Rings in Coq](https://hal.inria.fr/hal-01081908/document) doi:[10.2168/LMCS-12(2:7)2016](https://doi.org/10.2168/LMCS-12(2:7)2016)
  - [A refinement-based approach to large scale reflection for algebra](https://hal.inria.fr/hal-01414881/document) 

## Building and installation instructions

The easiest way to install the latest released version of CoqEAL
is via [OPAM](https://opam.ocaml.org/doc/Install.html):

```shell
opam repo add coq-released https://coq.inria.fr/opam/released
opam install coq-coqeal
```

To instead build and install manually, do:

``` shell
git clone https://github.com/coq-community/coqeal.git
cd coqeal
make   # or make -j <number-of-cores-on-your-machine> 
make install
```


## Theory

The theory directory has the following content:

- `ssrcomplements`, `minor` `mxstructure`, `polydvd`, `similar`,
  `binetcauchy`, `ssralg_ring_tac`: various extensions of the
  Mathematical Components library.

- `dvdring`, `coherent`, `stronglydiscrete`, `edr`: hierarchy of
  structures with divisibility (from rings with divisibility, PIDs,
  elementary divisor rings, etc.).

- `fpmod`: formalization of finitely presented modules.

- `kaplansky`: for providing elementary divisor rings from the
  Kaplansky condition.

- `bareiss_dvdring`, `bareiss`, `gauss`, `karatsuba`, `rank`
  `strassen` `toomcook`, `smithpid`, `smith`: various efficient
  algorithms for computing operations on polynomials or matrices.

## Refinements

The refinements directory has the following content:

- `refinements`: Classes for refinements and refines together with
  operational typeclasses for common operations.

- `binnat`: Proof that the binary naturals of Coq (`N`) is a refinement
  of SSReflect unary naturals (`nat`) together with basic operations.

- `binint`: SSReflect integers (`ssrint`) are refined to a new type
  paremetrized by positive numbers (represented by a sigma type) and
  natural numbers.  This means that proofs can be done using only
  lemmas from the SSReflect library which leads to simpler proofs than
  previous versions of `binint` (e.g., `N`).

- `rational`: The rational numbers of SSReflect (`rat`) is refined to
  pairs of elements refining integers using parametricity of
  refinements.

- `seqmatrix`: First and incomplete attempt to refine SSReflect
  matrices `M[R]_(m,n)`) to lists of lists (`seq (seq R)`).
  Work in progress.

- `seqpoly`: First and incomplete attempt to refine SSReflect
  polynomials (`{poly R}`) to lists (`seq R`). Work in progress.

Files should use the following conventions (w.r.t. `Local` and `Global` instances):

```coq
(** Part 1: Generic operations *)
Section generic_operations.

Global Instance generic_operation := ...

(** Part 2: Correctness proof for proof-oriented types and programs *)
Section theory.

Local Instance param_correctness : param ...

(** Part 3: Parametricity *)
Section parametricity.

Global Instance param_parametricit : param ...
Proof. exact: param_trans. Qed.

End parametricity.
End theory.
```
