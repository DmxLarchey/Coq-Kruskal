# The `Coq-Kruskal` project by [D. Larchey-Wendling](https://members.loria.fr/DLarchey/files)

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
- [`Kruskal-AlmostFull`](https://github.com/DmxLarchey/Kruskal-AlmostFull): the core library defining (inductivelly) the notions of almost full (AF) relations and bar predicates. The library recollects some results from \[2\] up to the constructive form of Ramsey's theorem (closure of AF relations under intersection), and as a consequence Dickson's lemma (closure of AF under direct products and direct sums). Additionally, it introduces the notion of surjective relational morphism to transfer the AF property.  
- [`Kruskal-Higman`](https://github.com/DmxLarchey/Kruskal-Higman): the detailed proof of Higman's lemma, ie the _homeomorphic embedding of lists is AF_, as an introduction to the proof of Veldman's theorem on the simpler case of unary trees (aka lists);   
- [`Kruskal-Veldman`](https://github.com/DmxLarchey/Kruskal-Veldman): the detailed proof of a variant of Veldman's theorem \[6\], which is the specific form he proposes for a direct inductive proof of Kruskal's theorem. Shares the same skeleton as [`Kruskal-Higman`](https://github.com/DmxLarchey/Kruskal-Higman) but in a much more complicated setting;
- [`Kruskal-Theorems`](https://github.com/DmxLarchey/Kruskal-Theorems): derives several instances of [Kruskal's tree theorem](https://en.wikipedia.org/wiki/Kruskal%27s_tree_theorem) from [`Kruskal-Veldman`](https://github.com/DmxLarchey/Kruskal-Veldman). Those proofs are much simpler as they just rely on surjective morphisms, the main difficulties being overcome in the proof of Veldman's theorem.

Side contributions and applications:
- the [`Karp-Miller`](https://github.com/DmxLarchey/Karp-Miller) algorithm for solving the [covering problem for Petri nets](https://en.wikipedia.org/wiki/Petri_net), of which termination is established using almost full relation, in particular, Coquand's version of Ramsey's theorem.
- [`Friedman-TREE`](https://github.com/DmxLarchey/Friedman-TREE): the construction of [Harvey Friedman's weak `Tree(n)` and `TREE(n)` functions](https://en.wikipedia.org/wiki/Kruskal%27s_tree_theorem) which are extremelly fast frowing functions that cannot be proved to exist in too weak meta-theories, eg Peano arithmetic.

## Historical remarks on the project

### Bibliographic references

- \[1\] [_A Constructive Proof of the Topological Kruskal Theorem_](https://doi.org/10.1007/978-3-642-40313-2_3) Jean Goubault-Larrecq.
- \[2\] [_Stop when you are Almost-Full: Adventures in constructive termination_](https://doi.org/10.1007/978-3-642-32347-8_17) Dimitrios Vytiniotis, Thierry Coquand, David Wahlstedt.
- \[3\] [_Kruskal’s Tree Theorem in a Constructive Theory of Inductive Definitions_](https://doi.org/10.1007/978-94-015-9757-9_21) Monika Seisenberger.
- \[4\] [_An Interpretation of the Fan Theorem in Type Theory_](https://doi.org/10.1007/3-540-48167-2_7) Daniel Firdlender
- \[5\] [_Higman's lemma in type theory_](https://doi.org/10.1007/BFb0097789) Daniel Firdlender
- \[6\] [_An intuitionistic proof of Kruskal's Theorem_](https://doi.org/10.1007/s00153-003-0207-x) Wim Veldman
- \[7\] [_About Brouwer’s Fan Theorem_](https://www.cairn-int.info/journal-revue-internationale-de-philosophie-2004-4-page-483.htm) Thierry Coquand
- \[8\] [_Higman’s Lemma and Its Computational Content_](https://doi.org/10.1007/978-3-319-29198-7_11) Helmut Schwichtenberg, Monika Seisenberger, Franziskus Wiesnet.

### The origins

The idea to implement a constructive proof of [Kruskal's tree theorem](https://en.wikipedia.org/wiki/Kruskal%27s_tree_theorem)
in Coq came to my mind in 2015. The statement of Kruskal's tree theorem concerns the closure properties of the notion of _Well Quasi Order_ (WQO). Classically characterized, a WQO `R : X → X → Prop` is a quasi order such that any infinite sequence `s : nat → X` contains a good (ie increasing pair), ie there are `i < j` such that `R sᵢ sⱼ`. However, constructivelly, this characterization is too weak (see below).  

Kruskal's tree theorem states: 

_<p style="text-align: center;">If a (base) relation is a WQO on a set of nodes, then the homeomorphic embedding it generates on finite trees build on those nodes is also a WQO.</p>_

The real motivation came after the reading of Jean Goubault-Larrecq's [_A Constructive Proof of the Topological Kruskal Theorem_](https://doi.org/10.1007/978-3-642-40313-2_3). Although it was the starting point; the approach developped in that paper was not followed in the end. According to Jean Goubault-Larrecq, it could not have led to the full result (that I wished for) because it implied assuming that the base relation on nodes was _decidable_. This constraint turned out to be the same assumption as the one made by Monika Seinsenberger in [her PhD thesis](https://doi.org/10.1007/978-94-015-9757-9_21). 

Then I turned to the work of people arround Thierry Coquand who characterized WQOs as _Almost Full_ (AF) relations using inductive predicates, either the specialized `af` predicate
```coq
Inductive af {X} (R : X → X → Prop) : Prop (or Type) :=
  | af_full : (∀ x y, R x y) → af R
  | af_lift : (∀ a, af (R↑a)) → af R
where "R↑a" := (λ x y, R x y ∨ R a x)
```
or the more general `bar` inductive predicate instantiated on the `good` predicate:
```coq
Inductive good {X} (R : X → X → Prop) : list X → Prop :=
  | good_stop x y l : y ∈ l → R y x → good R (x::l)
  | good_skip x l : good R l → good R (x::l).

Inductive bar {X} (P : list X → Prop) : list X → Prop (or Type) :=
  | bar_stop l : P l → bar P l
  | bar_next l : (∀x, bar P (x::l)) → bar P l.
```
Notice that the characterization of AF relations using sequences
```coq
Definition af_seq {X} (R : X → X → Prop) := ∀ s : nat → X, ∃ i j, i < j ∧ R sᵢ sⱼ
```
is weaker that the inductive characterization with eg `af R`. I later discovered this [beautiful intuition by Coquand](https://www.cairn-int.info/journal-revue-internationale-de-philosophie-2004-4-page-483.htm) \[7\] explaining why using sequences to characterizes WQOs or AF relations is problematic constructivelly: the issue comes from the _universal quantification over infinite sequences_ in the type `s : nat → X`, which constructivelly does not to cover sequences of which the enumeration is not given by a law (think of lambda terms).

IMHO, the best introduction the AF relations characterized with a specific inductive predicate can be found in [_Stop when you are Almost-Full: Adventures in constructive termination_](https://doi.org/10.1007/978-3-642-32347-8_17) by Coquand et al, of which the main contribution is a proof of constructive formulation of Ramsey's theorem:
```coq
Theorem af_inter {X} (R T : X → X → Prop) : af R → af T → af (R ∩ T).
```
However, this paper completely ignores the characterization using `bar` inductive predicates. This alternate characterization is used in Daniel Fridlender's work (a student of Coquand) in both [_An Interpretation of the Fan Theorem in Type Theory_](https://doi.org/10.1007/3-540-48167-2_7) and [_Higman's lemma in type theory_](https://doi.org/10.1007/BFb0097789). This last paper describes a constructive proof of [_Higman's lemma_](https://en.wikipedia.org/wiki/Higman%27s_lemma) avoiding the requirement of decidability. To my understanding, while it was not the first constructive proof of Higman's lemma, it was the first constructive proof of Higman's lemma avoiding the decidability asusmption. 

Fridlender's proof script is implemented in [ALF](https://en.wikipedia.org/wiki/ALF_(proof_assistant)), a predecessor of Agda.
ALF coding style is very much like Agda's but w/o infix notations, so the proof was somewhat hard to decifer. But I eventually did turn it into an Ltac style Coq proof, better suited for human readility.  Notice that the `bar` inductive characterization is also used/studied in [_Higman’s Lemma and Its Computational Content_](https://doi.org/10.1007/978-3-319-29198-7_11) by Seisenberger et al \[8\] and the explanations there also helped me better understand Fridlender's script.

At the time, by manipulating the two notions simultaneouly, I started to understand the equivalence between the `af R` characterization and the `bar (good R) []` characterization of almost full relations, which in turn can be proved relatively shortly after generalization:
`af (R↑xₙ...↑x₁) ↔ bar (good R) [x₁;...;xₙ]`.

After Higman's lemma, I naively tried to generalize the approach the binary trees instead of lists (which are just like unary trees). But Fridlender's proof scripts \[5\], or Seisenberger's btw \[8\], were way too much tailored to lists and I had great difficulty to abstract from that framework.

So I decided to study the only (published) intuitionistic proof of Kruskal's tree theorem avoiding the decidability issue: [_An intuitionistic proof of Kruskal's Theorem_](https://doi.org/10.1007/s00153-003-0207-x) by Wim Veldman \[6\]. I started to implement the proof of Higman's theorem to be found there, first on binary trees. Higman's theorem states that the nested product embedding is AF for tree of bounded breadth. This made me understand that Fridlender's and Seisenberger's proofs were just instances of Veldman's proof of Higman's theorem, adapted to type theory.

Veldman's proof however is not type theoretic. It is "formalized" in a kind of intuitionistic set theory but most data structures are encoded as natural numbers, which makes it quite an endavour to navigate. Also, the notion of AF relation used there is based on sequences, like `af_seq` above. To be able to work with this too weak notion, Veldman's postulates _Brouwer's thesis_, basically stating that if a relation is AF then there is a _stump_ that witnesses this property. I quickly understood that stumps were identical to the structure of inductive `af` predicate, representable as a _Well Founded Tree_ \[2\], and these could then be used as substitutes for Veldman's stumps:
```coq
Inductive WFT X :=
  | WFT_leaf : WFT X
  | WFT_node : (X → WFT X) → WFT X.

Fixpoint af_WFT {X} (R : X → X → Prop) (t : WFT X) : Prop :=
  match t with
  | WFT_leaf   => ∀ x y, R x y
  | WFT_node δ => ∀a, af_WFT (R↑a) (δ a)
  end.

Theorem af_WFT_equiv {X} (R : X → X → Prop) : af R ↔ {t | af_WFT R t}.
```
However the equivalence theorem `af_WFT_equiv` only holds (axiom free) when the `af R` predicate lives in sort `Type`, and not
when it leave in sort `Prop`. This means one cannot prove `af R → ∃t, af_WFT R t` when `af R : Prop` because this requires a variant of the axiom of choice. This may be one way to understand the use of Brouwer's thesis in the context of Coq type theory.

Hence I started to implement the proof of Higman's theorem found in \[6\] using the strong `af R : Type` notion, replacing
stumps with `WFT X` because those are needed there to implement lexicographic products. 

Veldman's tailored form of Kruskal's theorem, which I call Veldman's theorem in here, is restricted to relations over natural numbers `nat`, for several reasons: 
- the data-structure for rose trees is build over `nat`;
- Brouwer's thesis only applies to `nat`, ie it could be viewed as
```coq
Axiom Brouwers_thesis : ∀ (R : nat → nat → Prop), af_seq R → ∃ t : WFT nat, af_WFT R t.
```
- the proof requires embedding sub-trees into the nodes on other trees and the type `nat` allows such type theoretic constructions via encodings.

For my part, I did not want to restrict the end result to relations over only the type `nat`, or types that could be embedded into `nat`. So I started without this assumption to later realize how essential it was in Veldman's approach. Reflecting on this now, I realize that the project could have failed had I not tried this speculative generalization in the first place.

Indeed, all it took to generalize Veldman's proof from `nat` to another type `U : Type` was to realize that `U` should have thje properties of a _universe_. In the following sense: it should be stable under the type-theoretic constructs that occur in Veldman's proof. This turned out to be trivial to implement in Coq, as an inductive type: start with an abitrary type `X` and embed it into a larger universe `U` that contains `X` (one constructor), but which is also stable under some other type-theoretic constructs (eg 2 additional contructors).

This universe trick `U` lead me to the completion of Higman's theorem as in \[6\], proved w/o any axiom using the `Type` bounded version of the `af` predicate. The proof involved the manipulation of stumps as conveniently encoded in `WFT U`. Veldman/Kruskal's theorem somehow followed as its proof was based on the same sketch, but with twice more cases.

Switching to the `Prop` bounded version of `af` was much more tricky. Indeed, stumps are really needed to form lexicographic products which
are a foundational part of Veldman's proof. The reason why they are not needed for Higman's lemma \[5\] is because they can be inlined in the proof. Indeed, Higman's lemma is the instance of Higman's theorem where the bound on the arity of rose trees is `n=1`. In that case, the lexicographic induction on stumps can be implemented using `2` nested inductions, on `af R₁` and then on `af R₀`, where `Rᵢ` is the relation on nodes at arity `i=0` or `i=1`. This aproach is not feasible when the bound `n` on the arity is large or just an unknown constant.

To overcome this issue, I had to understand precisely how stumps where used in Veldman's proof. They served several purposes:
- certificates for the `af R` property via `af_WFT_equiv`;
- inductive data structures on which finitary lexicographic products could be formed;
- but also, critically, they served for discriminating when a relation was _full_, ie when the stump is `WFT_leaf`;
- and finally, there is also a use for stumps to represent when the sub-type of nodes is empty or not (not explained in here).

I did overlook last two purposes at first but understanding the role they played lead me search for alternatives that could serve as a replacement for stumps. It turns out that in complement to the `af Rᵢ` property, what is really needed is a mark to discriminate for when `Rᵢ : Xᵢ → Xᵢ → Prop` either live over an empty sub-type `Xᵢ`, or when `Rᵢ` is a full relation, or when we just know that `af Rᵢ` holds. This lead me to switch from stumps to AF witnesses: the data of a mark `wᵢ` and its property wrt `Xᵢ/Rᵢ`. Unfortunalety, AF witnesses do not have a proper well founded structure but, and this is the main insight, you can use them inductivelly to establish properties that do not talk about the witness `wᵢ`. I called this notion _well founded induction up to a projection_ and then proved that this notion is closed under lexicographic products.

Well founded induction up to a projection was the key that unlocked the case where `af R` is `Prop` bounded, allowing to dismiss Brouwer's thesis completely in Vedlman's proofs.

### Motivations for a reboot

Having completed a type theoretic implementation of Veldman's proof, getting rid of Brouwer's thesis on the way, was very satisfying at the time. Technically, the inductive implementation required some further assumptions, eg that the sub-types `Xᵢ` on then nodes were decidable. Some of these details are discussed in [`Kruskal-Veldman`](https://github.com/DmxLarchey/Kruskal-Veldman). But the final statement of Kruskal's theorem was the one I expected:
```coq
Theorem af_kruskal X (R : X → X → Prop) : af R → af (ltree_homeo_embed R).
```
which was quite satisfying indeed. 

But what do you do with a +30k loc Coq project with lots of redundancy and undecipherable proof scripts that only you can understand? 
- You have the satisfaction that Coq can type-check it as a valid and axiom free proof. This is undeniably your very first feeling after `Qed`.
- You can tell yourself: now people are going to be able to actually use Kruskal's theorem in their Coq proofs, to show termination of their fancy functions. However who really needs Kruskal's tree theorem for termination? **Recursive path orderings originally used it** but much shorter proofs were found later on. Ok [`Friedman-TREE`](https://github.com/DmxLarchey/Friedman-TREE) requires it but who is ever going to compute with this monster?
- You have the satisfaction of having intimatelly understood the inner workings of a complicated pen and paper proof, and even having improved it because of this understanding.
  
But you would like others to also understand this proof and, to that aim, have your code base serve as a guide and explanation, not as something which is even harder to understand than the original paper. 

### The split

### The end result
