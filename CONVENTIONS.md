# Conventions

This repo follows the published Rust guides instead of a house style:

- [Rust Style Guide](https://doc.rust-lang.org/style-guide/): formatting. `cargo fmt` applies it.
- [Rust API Guidelines](https://rust-lang.github.io/api-guidelines/): naming, API shape,
  documentation, interoperability.
- [Microsoft Pragmatic Rust Guidelines](https://microsoft.github.io/rust-guidelines/): libraries,
  applications, errors, safety, performance, documentation.

## Design

On top of the guides, write Rust roughly the way you would write Haskell:

1. **Push IO to the edges.** Decisions live in pure functions: data in, data out, for example
   `step(state, event) -> (state, effects)`. A thin shell reads the world, calls the core and
   carries out the effects it returns. No IO, clocks or threads inside the core.
   See [Functional Core, Imperative Shell](https://www.destroyallsoftware.com/screencasts/catalog/functional-core-imperative-shell)
   and [sans-IO](https://firezone.dev/blog/sans-io).
2. **Let types carry the facts.** Parse input once, at the edge, into types that only hold valid
   values, and don't check again past it. Use enums so impossible states can't be written.
   See [Parse, don't validate](https://lexi-lambda.github.io/blog/2019/11/05/parse-don-t-validate/)
   and [Type-Driven API Design in Rust](https://willcrichton.net/rust-api-type-patterns/).
3. **Judgement, not rules.** These are directions, not quotas. A `bool`, a `String` or a plain
   struct is fine when a type would add nothing. Don't add a newtype or a state machine that no
   bug and no reader needs.

The repo's own structure (crates, layers, where each concept lives) is in ARCHITECTURE.md.
