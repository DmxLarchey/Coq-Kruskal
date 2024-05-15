# The Coq-Kruskal project by [D. Larchey-Wendling](https://members.loria.fr/DLarchey/files)

## Summary

This repository only contains descriptions. In particular it does not contain code. 
The actual Coq code is scattered in [several sub-projects](#The-contents-of-sub-projects).

The `Coq-Kruskal` project was born after a complete rewrite of a [former constructive Coq proof 
of Kruskal's tree theorem](https://members.loria.fr/DLarchey/files/Kruskal) with the aim of
obtaining not only a computer certificate for the theorem, but mainly a proof that can be
studied by a (motivated enough) human. The Coq proof themselves have been factorized, abstracted
and minimized towards this target.

## The contents of sub-projects

List of sub-repositories of the core library:
- [`Kruskal-Trees`](https://github.com/DmxLarchey/Kruskal-Trees): definition for Coq data-structures for representing rose trees, including extensions or updates of the `List` and `Vector` modules of the standard library. Rose trees are viewed under several forms as nested inductive types (nested with `list` or `vec`) and provided with expressive recursors (induction principles);
- [`Kruskal-Finite`](https://github.com/DmxLarchey/Kruskal-Finite): a relativily compact library to manipulate the notion of finiteness of a type (resp. unary predicate), basically expressing the Coq computable existence of a list spanning exactly the type (resp. predicate). It allows to approach the notion of finiteness in an abstract and modular way; 
- [`Kruskal-AlmostFull`](https://github.com/DmxLarchey/Kruskal-AlmostFull): the core library defining (inductivelly) the notions of almost full (AF) relations and bar predicates. The library recollects some results from \[2\] up to the constructive form of Ramsey's theorem, and also introduces the notion of surjective relational morphism to transfer the AF property.  
- [`Kruskal-Higman`](https://github.com/DmxLarchey/Kruskal-Higman): the detailed proof of Higman's lemma, ie the _homeomorphic embedding of lists is AF_, as an introduction to the proof of Veldman's theorem on the simpler case of unary trees (aka lists);   
- [`Kruskal-Veldman`](https://github.com/DmxLarchey/Kruskal-Veldman): the detailed proof of a variant of Veldman's theorem \[6\], which is the specific form he proposes for a direct inductive proof of Kruskal's theorem. Shares the same skeleton as [`Kruskal-Higman`](https://github.com/DmxLarchey/Kruskal-Higman) but in a much more complicated setting;
- [`Kruskal-Theorems`](https://github.com/DmxLarchey/Kruskal-Theorems): derives several instances of [Kruskal's tree theorem](https://en.wikipedia.org/wiki/Kruskal%27s_tree_theorem) from [`Kruskal-Veldman`](https://github.com/DmxLarchey/Kruskal-Veldman). Those proofs are much simpler as they just rely on surjective morphisms, the main difficulties being overcome in the proof of Veldman's theorem.

Side contributions and applications:
- the [`Karp-Miller`](https://github.com/DmxLarchey/Karp-Miller) algorithm for solving the [covering problem for Petri nets](https://en.wikipedia.org/wiki/Petri_net), of which termination is established using almost full relation, in particular, Coquand's version of Ramsey's theorem.
- [`Friedman-TREE`](https://github.com/DmxLarchey/Friedman-TREE): the construction of [Harvey Friedman's weak `Tree(n)` and `TREE(n)` functions](https://en.wikipedia.org/wiki/Kruskal%27s_tree_theorem) which are extremelly fast frowing functions that cannot be proved to exist in too weak meta-theories, eg Peano arithmetic.

## Historical remarks on the project

### The origins

The idea to implement a constructive proof of [Kruskal's tree theorem](https://en.wikipedia.org/wiki/Kruskal%27s_tree_theorem)
in Coq came to my mind in 2015. The statement of Kruskal's tree theorem concerns the closure properties of the notion of _Well Quasi Order_ (WQO). Classically characterized, a WQO `R : X → X → Prop` is a quasi order such that any infinite sequence `s : nat → X` contains a good (ie increasing pair), ie there are `i < j` such that `R sᵢ sⱼ`. However, constructivelly, this characterization is too weak (see below).  

Kruskal's tree theorem states: 

_<p style="text-align: center;">If a (base) relation is a WQO on a set of nodes, then the homeomorphic embedding it generates on finite trees build on those nodes is also a WQO.</p>_

The real motivation came after the reading of Jean Goubault-Larrecq's [_A Constructive Proof of the Topological Kruskal Theorem_](https://doi.org/10.1007/978-3-642-40313-2_3). Although it was the starting point; the approach developped in that paper was not followed in the end. According to Jean Goubault-Larrecq, it could not have led to the full result (that I wished for) because it implied assuming that the base relation on nodes was _decidable_. This constraint turned out to be the same assumption as the one made by Monika Seinsenberger in [her PhD thesis](https://doi.org/10.1007/978-94-015-9757-9_21). 

Then I turned to the work of people arround Thierry Coquand who characterized WQOs as _Almost Full_ (AF) relations using inductive predicates, either the specialized `af` predicate or the more general `bar` inductive predicates. Notice that there are also characterizations of AF relations using sequences but they suffer the same issues as the classical characterization of WQOs. I later discovered this beautiful intuition by Coquand explaining why using sequences the characterizes WQOs or AF relations was **problematic constructivelly**. The problem comes from the universal quantification over sequence, which constructivelly is unable to capture sequence that are not governed by a law (aka a lambda term).

IMHO, the best introduction the AF relations characterized with a specific inductive predicate can be found in [_Stop when you are Almost-Full: Adventures in constructive termination_](https://doi.org/10.1007/978-3-642-32347-8_17) by Coquand et al, of which the main contribution is a proof of constructive formulation of Ramsey's theorem: the intersection of two AF relations is an AF relation. 

However, this paper completely ignores the characterization using `bar` inductive predicates. This alternate characterization is used in Daniel Fridlender's work (a student of Coquand) in both [_An Interpretation of the Fan Theorem in Type Theory_](https://doi.org/10.1007/3-540-48167-2_7) and [_Higman's lemma in type theory_](https://doi.org/10.1007/BFb0097789). This last paper describes a constructive proof of [_Higman's lemma_](https://en.wikipedia.org/wiki/Higman%27s_lemma) avoiding the requirement of decidability. To my understanding, while it was not the first constructive proof of Higman's lemma, it was the first constructive proof of Higman's lemma avoiding the decidability asusmption. 

Fridlender's proof script is implemented in [ALF](https://en.wikipedia.org/wiki/ALF_(proof_assistant)), a predecessor of Agda
ALF code is very much like Agda's but w/o notations, so the proof was quite hard to decifer. But I eventually did turn it into an Ltac style Coq proof, better suited for human readility.  Notice that the `bar` inductive characterization is also used/studied in [_Higman’s Lemma and Its Computational Content_](https://doi.org/10.1007/978-3-319-29198-7_11) by Seisenberger et al and the explanations there helped me better understand Fridlender's script.

At the time, by manipulating the two notions simultaneouly, I started to understand the equivalence between the `af R` characterization and the `bar (good R) []` characterization of almost full relations, which in turn can be proved relatively shortly.

After Higman's lemma, I naively tried to generalize the approach the binary trees instead of lists (which are just like unary trees). But Fridlender's proof scripts, or Seisenberger's btw, where way too much tailored to lists and I had great difficulty to abstract from that framework.

So I decided to study the only (published) intuitionistic proof of Kruskal's tree theorem avoiding the decidability issue: [_An intuitionistic proof of Kruskal's Theorem_](https://doi.org/10.1007/s00153-003-0207-x) by Wim Veldman. I started to implement the proof of Higman's theorem to be found there, first on binary trees. Higman's theorem states that the nested product embedding is AF for tree of bounded breadth. This made me understand that Fridlender's and Seisenberger's proofs were just instances of Veldman's proof of Higman's tree, adapted to type theory.

Veldman's proof is not type theoretic. It is "formalized" in a kind of intuitionistic set theory but most data structures are encoded as natural numbers, which makes it quite hard to decifer. Also, the notion of AF relation used there is based on sequences. To be able to work with this too weak notion, Veldman's postulates _Brouwer's thesis_, basically stating that if a relation is AF then there is a _stump_ that witnesses this property. I immediatly recognised that stumps were identical to the structure of inductive `af` predicate, representable as a _well founded tree_.

- \[1\] [_A Constructive Proof of the Topological Kruskal Theorem_](https://doi.org/10.1007/978-3-642-40313-2_3) Jean Goubault-Larrecq.
- \[2\] [_Stop when you are Almost-Full: Adventures in constructive termination_](https://doi.org/10.1007/978-3-642-32347-8_17) Dimitrios Vytiniotis, Thierry Coquand, David Wahlstedt.
- \[3\] [_Kruskal’s Tree Theorem in a Constructive Theory of Inductive Definitions_](https://doi.org/10.1007/978-94-015-9757-9_21) Monika Seisenberger.
- \[4\] [_An Interpretation of the Fan Theorem in Type Theory_](https://doi.org/10.1007/3-540-48167-2_7) Daniel Firdlender
- \[5\] [_Higman's lemma in type theory_](https://doi.org/10.1007/BFb0097789) Daniel Firdlender
- \[6\] [_An intuitionistic proof of Kruskal's Theorem_](https://doi.org/10.1007/s00153-003-0207-x) Win Veldman

### Motivations for a reboot

### the split

### the end result
