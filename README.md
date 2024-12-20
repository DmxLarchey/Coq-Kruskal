# The `Coq-Kruskal` project by [D. Larchey-Wendling](https://members.loria.fr/DLarchey/files)

## Summary

This repository only contains descriptions. In particular it does not contain code. 
The actual Coq code is scattered in [several sub-projects (see below)](#The-contents-of-sub-projects).

The `Coq-Kruskal` project was born after a complete rewrite of a [former constructive Coq proof 
of Kruskal's tree theorem](https://members.loria.fr/DLarchey/files/Kruskal) with the aim of
obtaining not only a computer certificate for the theorem, but mainly carefully structured proof that can be
studied by a (motivated enough) human. The Coq statements and proof scripts themselves have been factorized, abstracted
and minimized towards this target.

## The contents of sub-projects

List of sub-repositories of the core library:
- [`Kruskal-Trees`](https://github.com/DmxLarchey/Kruskal-Trees): definitions for Coq data-structures for representing rose trees, including extensions or updates of the `List` and `Vector` modules of the standard library. Rose trees are viewed under several forms as nested inductive types (nested with `list` or `vec`) and provided with expressive recursors (ie. induction principles);
- [`Kruskal-Finite`](https://github.com/DmxLarchey/Kruskal-Finite): a relativily compact library to manipulate the notion of finiteness of a type (resp. unary predicate), basically expressing the Coq computable existence of a list spanning exactly the type (resp. predicate). It allows to approach the notion of finiteness in an abstract, dependent and modular way; 
- [`Kruskal-AlmostFull`](https://github.com/DmxLarchey/Kruskal-AlmostFull): the core library defining (inductivelly) the notions of almost full (AF) relations and bar predicates. The library recollects some results from \[2\] up to the constructive form of Ramsey's theorem (closure of AF relations under intersection), and as a consequence Dickson's lemma (closure of AF under direct products and direct sums). Additionally, it introduces the notion of surjective relational morphism to transfer the AF property.
- [`Kruskal-Fan`](https://github.com/DmxLarchey/Kruskal-Fan): the FAN theorem for monotone inductive bars and a constructive variant of König's lemma;
- [`Kruskal-Higman`](https://github.com/DmxLarchey/Kruskal-Higman): the detailed proof of Higman's lemma, ie the _homeomorphic embedding of lists is AF_, as an introduction to the proof of Veldman's theorem on the simpler case of unary trees (aka lists);   
- [`Kruskal-Veldman`](https://github.com/DmxLarchey/Kruskal-Veldman): the detailed proof of a variant of Veldman's theorem \[6\], which is the specific form he proposes for a direct inductive proof of Kruskal's theorem. Shares the same skeleton as [`Kruskal-Higman`](https://github.com/DmxLarchey/Kruskal-Higman) but in a much more complicated setting;
- [`Kruskal-Theorems`](https://github.com/DmxLarchey/Kruskal-Theorems): derives several instances of [Kruskal's tree theorem](https://en.wikipedia.org/wiki/Kruskal%27s_tree_theorem) from [`Kruskal-Veldman`](https://github.com/DmxLarchey/Kruskal-Veldman). Those proofs are much simpler as they just rely on surjective morphisms, the main difficulties being overcome in the proof of Veldman's theorem.

Side contributions and applications:
- [`Quasi-Morphisms`](https://github.com/DmxLarchey/Quasi-Morphisms): standalone explanations on [how to transfert AF between relations](https://easychair.org/publications/preprint/M3Km), as used in the proofs of [`Kruskal-Higman`](https://github.com/DmxLarchey/Kruskal-Higman) and [`Kruskal-Veldman`](https://github.com/DmxLarchey/Kruskal-Veldman);
- the [`Karp-Miller`](https://github.com/DmxLarchey/Karp-Miller) algorithm for solving the [covering problem for Petri nets](https://en.wikipedia.org/wiki/Petri_net), of which termination is established using almost full relation, in particular, Coquand's version of Ramsey's theorem;
- [`Friedman-TREE`](https://github.com/DmxLarchey/Friedman-TREE): the construction of [Harvey Friedman's weak `Tree(n)` and `TREE(n)` functions](https://en.wikipedia.org/wiki/Kruskal%27s_tree_theorem) which are extremelly fast frowing functions that cannot be proved to exist in too weak meta-theories, eg Peano arithmetic;
- [`Relevant-decidability`](https://github.com/DmxLarchey/Relevant-decidability) a standalone constructive proof of the decidability of _Implicational Relevance Logic_ \[10\] using AF versions of Ramsey's theorem and König's lemma, as also found in [`Kruskal-AlmostFull`](https://github.com/DmxLarchey/Kruskal-AlmostFull) and [`Kruskal-Fan`](https://github.com/DmxLarchey/Kruskal-Fan).

## Bibliographic references

- \[1\] [_A Constructive Proof of the Topological Kruskal Theorem_](https://doi.org/10.1007/978-3-642-40313-2_3) Jean Goubault-Larrecq.
- \[2\] [_Stop when you are Almost-Full: Adventures in constructive termination_](https://doi.org/10.1007/978-3-642-32347-8_17) Dimitrios Vytiniotis, Thierry Coquand, David Wahlstedt.
- \[3\] [_Kruskal’s Tree Theorem in a Constructive Theory of Inductive Definitions_](https://doi.org/10.1007/978-94-015-9757-9_21) Monika Seisenberger.
- \[4\] [_An Interpretation of the Fan Theorem in Type Theory_](https://doi.org/10.1007/3-540-48167-2_7) Daniel Fridlender
- \[5\] [_Higman's lemma in type theory_](https://doi.org/10.1007/BFb0097789) Daniel Fridlender
- \[6\] [_An intuitionistic proof of Kruskal's Theorem_](https://doi.org/10.1007/s00153-003-0207-x) Wim Veldman
- \[7\] [_About Brouwer’s Fan Theorem_](https://www.cairn-int.info/journal-revue-internationale-de-philosophie-2004-4-page-483.htm) Thierry Coquand
- \[8\] [_Higman’s Lemma and Its Computational Content_](https://doi.org/10.1007/978-3-319-29198-7_11) Helmut Schwichtenberg, Monika Seisenberger, Franziskus Wiesnet.
- \[9\] [_Quasi Morphisms for Almost Full Relations_](https://easychair.org/publications/preprint/M3Km) Dominique Larchey-Wendling.
- \[10\] [_Constructive Decision via Redundancy-free Proof-Search_](http://www.loria.fr/~larchey/papers/JAR-2019.pdf) Dominique Larchey-Wendling.

## Historical remarks on the project

### The origins

The idea to implement a constructive proof of [Kruskal's tree theorem](https://en.wikipedia.org/wiki/Kruskal%27s_tree_theorem)
in Coq came to my mind in 2015. The statement of Kruskal's tree theorem concerns the closure properties of the notion of _Well Quasi Order_ (WQO). Classically characterized, a WQO `R : rel₂ X` (where `rel₂ X := X → X → Prop`) is a quasi order such that any infinite sequence `s : nat → X` contains a good (ie increasing pair), ie there are `i < j` such that `R sᵢ sⱼ`. However, constructivelly, this characterization is too weak (see below).  

Kruskal's tree theorem states: 

_<p style="text-align: center;">If a (base) relation is a WQO on a set of nodes, then the homeomorphic embedding it generates on finite trees build on those nodes is also a WQO.</p>_

But for me, the real motivation came after reading Jean Goubault-Larrecq's [_A Constructive Proof of the Topological Kruskal Theorem_](https://doi.org/10.1007/978-3-642-40313-2_3) \[1\]. Although it was the starting point; the approach developped in that paper was not followed in the end. According to Jean Goubault-Larrecq, it could not have led to the full result (that I wished for) because it implied assuming that the base relation on nodes was _decidable_. This constraint turned out to be the same assumption as the one made by Monika Seinsenberger in [her PhD thesis](https://doi.org/10.1007/978-94-015-9757-9_21) \[3\]. 

Then I turned to the work of people arround Thierry Coquand who characterized WQOs as _Almost Full_ (AF) relations using inductive predicates, either the specialized `af` predicate
```coq
Inductive af {X} (R : rel₂ X) : Prop (or Type) :=
  | af_full : (∀ x y, R x y) → af R
  | af_lift : (∀ a, af (R↑a)) → af R
where "R↑a" := (λ x y, R x y ∨ R a x)
```
or the more general `bar` inductive predicate instantiated on the `good` predicate as `bar (good R) []`:
```coq
Inductive good {X} (R : rel₂ X) : list X → Prop :=
  | good_stop x y l : y ∈ l → R y x → good R (x::l)
  | good_skip x l : good R l → good R (x::l).

Inductive bar {X} (P : list X → Prop) : list X → Prop (or Type) :=
  | bar_stop l : P l → bar P l
  | bar_next l : (∀x, bar P (x::l)) → bar P l.
```
Notice that the characterization of AF relations using infinite sequences in `nat → X`
```coq
Definition af_seq {X} (R : rel₂ X) := ∀ s : nat → X, ∃ i j, i < j ∧ R sᵢ sⱼ
```
is weaker that the inductive characterization with eg `af R`. I later discovered this [beautiful intuition by Coquand](https://www.cairn-int.info/journal-revue-internationale-de-philosophie-2004-4-page-483.htm) \[7\] explaining why using sequences to characterizes WQOs or AF relations is problematic constructivelly: the issue comes from the _universal quantification over infinite sequences_ in the type `s : nat → X`, which constructivelly does not to cover sequences of which the enumeration is not given by a law (think of lambda terms).

IMHO, the best introduction to AF relations characterized with a specific inductive predicate can be found in [_Stop when you are Almost-Full_](https://doi.org/10.1007/978-3-642-32347-8_17) by Coquand et al \[2\], of which the main contribution is a proof of a constructive formulation of Ramsey's theorem:
```coq
Theorem af_inter {X} (R T : rel₂ X) : af R → af T → af (R ∩ T).
```
However, this paper completely skips the characterization using `bar` inductive predicates. This alternate characterization is used in Daniel Fridlender's work (a student of Coquand) in both [_An Interpretation of the Fan Theorem in Type Theory_](https://doi.org/10.1007/3-540-48167-2_7) \[4\] and [_Higman's lemma in type theory_](https://doi.org/10.1007/BFb0097789) \[5\]. This last paper describes a constructive proof of [_Higman's lemma_](https://en.wikipedia.org/wiki/Higman%27s_lemma) avoiding the requirement of decidability. To my understanding, while it was not the first constructive proof of Higman's lemma, it was the first constructive proof of Higman's lemma avoiding the decidability assumption. 

Fridlender's proof script is implemented in [ALF](https://en.wikipedia.org/wiki/ALF_(proof_assistant)), a predecessor of Agda.
ALF coding style is very much like Agda's but w/o infix notations, so the proof was somewhat hard to decifer. But I eventually did turn it into an Ltac style Coq proof, better suited for human readility.  Notice that the `bar` inductive characterization is also used/studied in [_Higman’s Lemma and Its Computational Content_](https://doi.org/10.1007/978-3-319-29198-7_11) by Seisenberger et al \[8\] and the explanations there also helped me better understand Fridlender's script.

At the time, by manipulating the two notions simultaneouly, I started to grasp the _equivalence_ between the `af R` characterization and the `bar (good R) []` characterization of almost full relations, which in turn can be proved relatively shortly after generalization:
`af (R↑xₙ...↑x₁) ↔ bar (good R) [x₁;...;xₙ]`.

After rewriting the proof of Higman's lemma \[5,8\], I naively tried to generalize the approach to binary trees instead of lists (which are just like unary trees). But Fridlender's proof scripts \[5\], or Seisenberger's btw \[8\], were way too much tailored to lists and I had great difficulty to abstract from that framework.

So I decided to study the only (published) intuitionistic proof of Kruskal's tree theorem avoiding the decidability issue: [_An intuitionistic proof of Kruskal's Theorem_](https://doi.org/10.1007/s00153-003-0207-x) by Wim Veldman \[6\]. I started to implement the proof of Higman's theorem to be found there, first on binary trees. Higman's theorem states that the nested product embedding is AF for tree of bounded breadth. This made me understand that Fridlender's and Seisenberger's proofs were just instances of Veldman's proof of Higman's theorem, adapted to type theory.

Veldman's proof however is not type theoretic. It is "formalized" in a kind of intuitionistic set theory but most data structures are encoded as natural numbers, which makes it quite an endavour to navigate. Also, the notion of AF relation used there is based on sequences, like `af_seq` above. To be able to work with this too weak notion, Veldman's postulates _Brouwer's thesis_, basically stating that if a relation is AF then there is a _stump_ that witnesses this property. I quickly understood that stumps were identical to the structure of inductive `af` predicate, representable as a _Well Founded Tree_ \[2\], and these could then be used as substitutes for Veldman's stumps:
```coq
Inductive WFT X :=
  | WFT_leaf : WFT X
  | WFT_node : (X → WFT X) → WFT X.

Fixpoint af_WFT {X} (R : rel₂ X) (t : WFT X) : Prop :=
  match t with
  | WFT_leaf   => ∀ x y, R x y
  | WFT_node δ => ∀a, af_WFT (R↑a) (δ a)
  end.

Theorem af_WFT_equiv {X} (R : rel₂ X) : af R ↔ {t | af_WFT R t}.
```
However the equivalence theorem `af_WFT_equiv` only holds (axiom free) when the `af R` predicate lives in sort `Type`, and not
when it leave in sort `Prop`. This means one cannot prove `af R → ∃t, af_WFT R t` when `af R : Prop` because this requires a variant of the axiom of choice. This may be one way to understand the use of Brouwer's thesis in the context of Coq type theory.

Hence I started to implement the proof of Higman's theorem found in \[6\] using the strong `af R : Type` notion, replacing
stumps with `WFT X` because those are needed there to implement lexicographic products. 

Veldman's tailored form of Kruskal's theorem, which I call Veldman's theorem in here, is restricted to relations over natural numbers `nat`, for several reasons: 
- the data-structure for rose trees is build over `nat`;
- Brouwer's thesis only applies to `nat`, ie it could be viewed as
```coq
Axiom Brouwers_thesis : ∀ (R : rel₂ nat), af_seq R → ∃ t : WFT nat, af_WFT R t.
```
- the proof requires embedding sub-trees into the nodes on other trees and the type `nat` allows such type theoretic constructions via encodings.

For my part, I did not want to restrict the end result to relations over the type `nat` only, or over types that could be embedded into `nat`. So I started without this assumption to later discover how essential it was in Veldman's approach. Reflecting on this now, I realize that the project could have failed had I not tried this speculative generalization in the first place.

Indeed, all it took to generalize Veldman's proof approach from `nat` to another type `U : Type` was to understand that `U` should have the properties of a __universe__ (in the following sense): it should be _stable under the type-theoretic constructs that occur in Veldman's proof_. This turned out to be trivial to implement in Coq, using an inductive type: start with an abitrary type `X` and embed it into a larger universe `U` that contains `X` (one constructor), but which is also stable under some other type-theoretic constructs (typically 2 additional contructors).

This universe trick `U` lead me to the completion of Higman's theorem as in \[6\], first proved w/o any axiom using the `Type` bounded version of the `af` predicate. The proof involved the manipulation of stumps as conveniently encoded in `WFT U`. Veldman/Kruskal's theorem somehow followed as its proof was based on the same sketch, but with twice more cases.

Switching to the `Prop` bounded version of `af` was trickier. Indeed, stumps are really needed to form lexicographic products which
are a essential part of Veldman's inductive argument. The reason why they are not needed for Higman's lemma \[5\] is because they can be somehow inlined in the proof. Indeed, Higman's lemma is the instance of Higman's theorem where the bound on the arity of rose trees is `n=1`. In that case, the lexicographic induction on stumps can be implemented using `2` nested inductions, on `af R₁` and then on `af R₀`, where `Rᵢ` is the relation on nodes at arity `i=0` or `i=1`. This aproach is not feasible when the bound `n` on the arity is large or just an unknown constant.

To overcome this issue that occurs only in the `Prop` bounded variant, I had to understand precisely how stumps where used in Veldman's approach. They served several purposes:
- certificates for the `af R` property via `af_WFT_equiv`;
- inductive data structures on which finitary lexicographic products could be formed;
- but also, critically, they served for discriminating when a relation was _full_, ie when the stump is `WFT_leaf`;
- and finally, there is also a use for stumps to represent when the sub-type of nodes is empty or not (not explained in here).

I did overlook the last two purposes at first but understanding the role they played lead me search for alternatives that could serve as a replacement for stumps. It turns out that in complement to the `af Rᵢ` property, what is really needed is a mark to discriminate for when `Rᵢ : rel₂ Xᵢ` either live over an empty sub-type `Xᵢ`, or when `Rᵢ` is a full relation, or when we just know that `af Rᵢ` holds. 

This lead me to switch from stumps to AF witnesses: the data of a mark `wᵢ` and its property wrt `Xᵢ/Rᵢ`. Unfortunalety, AF witnesses do not have a proper well founded structure, but, _and this is the main insight_, you can use them inductivelly to establish properties of `Xᵢ/Rᵢ` that do not talk about the witness `wᵢ`. I did call this notion _well founded induction up to a projection_ and then proved that it is closed under lexicographic products.

Well founded induction up to a projection was the key that unlocked Veldman's approach, also in the case where `af R` is `Prop` bounded, allowing to dismiss Brouwer's thesis completely in my implementation of Veldman's proofs.

### Motivations for a reboot

Having completed a type theoretic implementation of Veldman's proof, getting rid of Brouwer's thesis on the way, was very satisfying at the time. Technically, the inductive implementation required some further assumptions, eg that the sub-types `Xᵢ` on then nodes of arity `i` were decidable. Some of these details are discussed in [`Kruskal-Veldman`](https://github.com/DmxLarchey/Kruskal-Veldman). But the final statement of Kruskal's theorem was the one I expected:
```coq
Theorem af_kruskal X (R : rel₂ X) : af R → af (ltree_homeo_embed R).
```
which was quite satisfying. 

But what do you do with a +30k loc Coq project with lots of redundancies and undecipherable proof scripts that only you can understand? 
- You have the satisfaction that Coq can type-check it as a valid and axiom-free proof. This is undeniably your very first feeling after `Qed`.
- You can tell yourself that people are going to be able to actually use Kruskal's theorem in their Coq proofs, to show termination of their fancy functions. However who really needs Kruskal's tree theorem for termination? [Recursive path orderings originally used it](https://doi.org/10.1016/0304-3975(82)90026-3) but much shorter and direct constructive proofs were found later on. Of course [`Friedman-TREE`](https://github.com/DmxLarchey/Friedman-TREE) requires it, but who is ever going to compute with this monster?
- You have the satisfaction of having intimatelly understood the inner workings of a complicated pen and paper proof, and even having improved it because of this understanding.
  
But you would like others to also understand this proof and, to that aim, have your code base serve as a guide and explanation, not as something which is even harder to understand than the original pen&paper proof \[6\]. I tried several to document the proof in the form of a paper but each attempt turned out to miss what I was aiming for, a understandable guide of the mechanized proof.

Several years later, arround late 2021, but also, many more line of Coq code later, devoted to others projects, some of them exploiting parts of the ideas present in the [initial mechanization](https://members.loria.fr/DLarchey/files/Kruskal) like how to smoothly work with rose trees in Coq or how work with `bar` inductive predicates or the `Acc`essibility predicate, but also after sensibly enhancing my skill working with dependent types and dependent pattern matching, I decided to rewrite the whole project with the following ideas:
- a much improved factorization of the code, avoiding completely coding duplications:
    - for instance, the `Prop`-bounded and `Type`-bounded version now share the very same code base. There is a compilation switch that generates one version or the other from the same scripts;
    - the inductive proof Higman's theorem has been removed and replaced with an instance of Veldman/Kruskal's theorem which avoids duplicating two very similar proofs.
- replacing quasi-morphisms with a relational version of these allowed to drop the decidabilty assumption on sub-types of nodes `Xᵢ : U → Prop`, allowing the removal of large amounts of now unnecessary proofs and assumptions;
- replacing `list`s with `vec`tors to collect the sons in rose trees allowed for a much better control of side conditions, at the level of typing, allowing the simplify the construction of quasi-morphisms, and in particular, of finiteness proofs;
- a abstracted approach, dependently typed, allowed for much shortened proofs of finiteness, replacing explicit constructions of spanning lists by hand;
- a structured code base with better automation and shorter independent proofs that allow for a modular analysing of the proofs:
    - the longests proofs to be found, [eg those related to quasi-morphisms](https://github.com/DmxLarchey/Kruskal-Veldman/blob/3b1231dc4b49327bcbdfcf3c9bf868916f34ae7a/theories/universe/veldman_kruskal.v#L614), are now less that 70 locs, which is reasonable, compared to the initial project where single proofs weighting above 500 locs were not uncommon;
    - eventually, this structure favored a split of the code base into several sub-project that could be used somewhat independently.

### The split

Late 2022 I was contacted by [J. Hughes](http://www.jerome-hugues.net/) because he needed to work with rose trees, and he found the tools that were developped for the [initial mechanization of Kruskal's tree theorem](https://members.loria.fr/DLarchey/files/Kruskal) to be useful for what he wanted. Given that this version was unmaintained, he asked whether I had updated the code base for up to date versions of Coq and if I could share this code.

I did allow him to access the reboot project and then, he asked if the project could be made public so that he could reuse the work and properly reference its source. I decided to split the project and publish the part of it that dealt with the data-types for rose trees, and its dependecies, in the independent project now called [_Kruskal-Trees_](https://github.com/DmxLarchey/Kruskal-Trees).

Half a year later, meeting with the team of [J. Leroux](https://www.labri.fr/perso/leroux/) in Bordeaux to discuss applications of AF relations to Petri nets and the computation of [Karp-Miller coverings](https://github.com/DmxLarchey/Karp-Miller), they asked whether the library that coped with finiteness wouldn't also be of independent interest. With lead sometimes later to the creating of [`Kruskal-Finite`](https://github.com/DmxLarchey/Kruskal-Finite). 

These moves were accompanied to the publication of those sub-libraries as [`opam` packages](https://github.com/coq/opam) for much easier deployment by outsider. Finally, late 2023, I decided that it was time to split the whole project into a satisfying hierarchy of packages, also distributed as `opam` packages. These packages are also individualy documented.

### The paper

It is now time to write a paper about this work. Here are some ideas for the content:
- it should not reproduce Veldman's proofs, but instead limit itself to the general structure of proofs
- it *must* explain why and how some issues in Veldman's proof were solved:
    - not working with the base type `nat` only;
    - avoiding _Brouwer's thesis_;
    - replacing the sequence based definition of AF with the inductive version
    - abstracting quasi-morphisms;
    - well-foundedness upto
