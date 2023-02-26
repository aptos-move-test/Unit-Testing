# Unit-Testing

Unit testing in Move provides three ways to test in the Move Source language.

- `#[test]`
- `#[test_only]`, and
- `#[expected_failure]`.

`#[test]` and `#[expected_failure]` are commonly used with or without any arguments.

`#[test]` can only be used on functions without any parameters. It simply marks the function as a test to run during unit testing.

```rust
#[test] 
fun Let's_do_a_test() { ... }

#[test] // It Will fail to compile since this test takes an argument
fun Can't_use_in_this_format(arg: signer) { ... }
```

`#[expected_failure]` defines that certain tests are expected to raise certain errors so it can skip or abort them during testing. It can be used by using the abort command such as `#[expected_failure(abort_code = <code>)]`. If a function has `#[test]` test case, only `#[expected_failure]` can be used.

```rust
#[test]
#[expected_failure]
public fun It_will_abort_this_test_and_pass() { abort 1 }

#[test]
#[expected_failure]
public fun test_will_get_error_and_pass() { 1/0; }

#[test]
#[expected_failure(abort_code = 0)]
public fun test_will_get_error_and_fail() { 1/0; }

#[test, expected_failure] // It can have multiple in a single attribute. It will pass this test.
public(script) fun test_will_abort_and_pass() { abort 1 }
```
