## Core ideas
- simple code should be short to write
- vocabulary should be short and concise -- no two ways to do something
- constants can be produced by functions, they should be evaluated at compile time
- statically and strongly typed
- functional -> only functions and data
- switch statements for everything
- arbitrary percision numbers (ints and floats)
- piping syntax
- pure functions evaluated at compile time

## Some examples

### Sign function

```
type Sign {
  Positive
  Negative
  Zero
}

fn sign(
  number: Int,
): Sign {
  when number {
    x if x > 0 -> Positive
    x if x < 0 -> Negative
    else -> Zero
  }
}

pub fn main(): Effect<Unit> {
  sign(73)
  |> io.println
}
```

### Compile time regex

```
const simple_email_regex = regex.compile("^[\w-\.]+@([\w-]+\.)+[\w-]{2,4}$")

fn validate_email(
  input: String,
): Result<Unit, Unit> {
  ... regex.match(simple_email_regex, in: input)
  ...
  Ok
}
```

### Ternary using switch

```
fn basic(x: Int): Int {
  when x % 2 == 0 {
    True -> x + 2
    False -> x * 2
  }
}
```

### Effects and pure FFIs

Functions are pure by default. You can add FFIs and external implementations, but these are treated as impure by default, and will return `Effect<?>`.

```
@impl(javascript, "console", "log")
fn println(value: String): Effect<Unit>
```

If you want to wire in an external implementation that you are 100% certain is pure, you can mark it as such.

```
@pure_impl(javascript, "Math", "sqrt")
fn sqrt(x: Int): Float
```

Note to self -- should this be a warning, or auditable, or ...?



