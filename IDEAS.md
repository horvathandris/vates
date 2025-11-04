## Core ideas
- simple code should be short to write
- vocabulary should be short and concise -- no two ways to do something
- constants can be produced by functions, they should be evaluated at compile time
- statically and strongly typed
- functional -> only functions and data
- switch statements for everything
- arbitrary percision numbers (ints and floats)
- piping syntax

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

pub fn main(): Unit {
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
}
```
