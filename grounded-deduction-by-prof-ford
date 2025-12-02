# Grounded Deduction — Notes

**Grounded Deduction (GD)**  
→ weakening **LEM** (طرد شق ثالث) to focus on **consistency** and **recursive definition** (the “impossible triangle”).

---

## Curry’s Paradox
An *if* condition where the **مقدم** is self-referring, so it cannot be trusted to be true.  
But by assuming it *is* true, we can deduce its **تالی** to be true as well.

---

## “Habeas quid”
Meaning: *we must have a thing before we use it* (وجود شاهد).  
This law does **not** exist in classical logic, but GD applies it systematically.

---

## Kleene’s Three-Valued Logic
Includes an extra proposition that is neither true nor false.

In GD:

> “A proposition by default has no value of any type.”

Very interesting — there’s not even a distinction between **terms** and **sentences** until typing is established.

---

## Syntax View in GD
Everything remains **untyped** until a grounded process proves it to be of type *x*.

Examples:

- `a B` → introducing `a` as a Boolean (similar to type theory's `a : B`)
- `a T → a B`
- `a F → a B`

Elimination example:

a B, (a F → c T), (a T → c T) → c T (مثل همون حذف فصل)


Special case `c := a`:  
This gives a **proof by contradiction**, but with the limitation that `a` must be Boolean.

As in classical logic:  
a Boolean cannot be both `T` and `F`, so contradiction implies `c T` for any `c`.

---

## Note to Self
`trueIE` seems odd; revisit this later.

Currently the use of `c → c T` feels like a violation of *habeas quid*:  
when did we prove `c` is of type `True`?

Interpretation: anything that has been *introduced* exists as “true.”  
This aligns with type theory.

But still, not everything is a Boolean — GD’s point was avoiding the “original sin” of premature truth assignment.

---

## Negation
We have:

!a F → a T


Equivalent to **RAA**, but again restricted to values already proven to be Boolean.

We use an arbitrary `c` not in our **فرض**s to deduce `a F`.  
(مثل همون حذف فصلی که چون آ بولینه و از درستیش میشه به درستی یچیز دلخواه رسید،
میشه به درستی نات آ رسید و از آ فالس هم میشه به درستی نات آ رسید.
انگار اینجا داریم معرفی به ازای هر می‌زنیم)

Double-negation elimination is also present.  
So classical logic embeds cleanly inside GD.

---

## Equality
Equality exists “indirectly” by introducing a new unused constant.  
Existential elimination works as in classical logic.

Crucially, the constant must be *introduced first*, preventing the liar paradox:  
you cannot assert `L = !L`.

---

## Connectives: AND / OR
The semantics of `∧` and `∨` are introduced as follows:

- For **T**, same as classical logic  
- For **F**, rules are inverted, e.g.:

  - `b F → a ^ b F`
  - `(a ^ b F)` elimination behaves like `(a v b T)` elimination (same as classical VE)

Since double-negation elimination and correct semantic rules are preserved, **De Morgan’s laws hold** in GD.

---

**End of Page 17**
