---
title: hspec
language: haskell
---

# {{ page.title }}

Codewars supports [hspec](https://hackage.haskell.org/package/hspec-meta-1.10.0),
a BDD test framework for Haskell modeled after
Ruby's popular [Rspec](http://rspec.info/) framework.

For more information, see: <http://hspec.github.io>.

## Setup

A minimal test fixture looks as follows:

Solution Code:

```haskell
module Haskell.Codewars.Greeter where
import Text.Printf (printf)

data Greeter = Greeter String

greet :: Greeter -> String -> String
greet (Greeter name) otherName =
  printf "Greetings!  I am %s.  Welcome, %s!" name otherName
```

**_NOTE_**:
It is always necessary to have a `module` declaration in your solution code, so it can be imported elsewhere.
_Try to have unique module names, to avoid name collisions._

Test Fixture:

```haskell
import Test.Hspec
import Haskell.Codewars.Greeter

main :: IO ()
main = hspec $ do
  describe "Testing Greeter" $
    it "Shoki meets Su Kong Tai Djin" $ do
      -- ...IO Monad Actions...
      let shoki = Greeter "Shoki, the Demon Queller"
      putStrLn "Greeting Tai Djin..."
      let taiDjin = "Grandmaster Su Kong Tai Djin"
      -- Final expression should have type signature `IO ()`
      (shoki `greet` taiDjin) `shouldBe`
        "Greetings!  I am Shoki, The Demon Queller.  Welcome, Grandmaster Su Kong Tai Djin!"
```

In Hspec, `Expectation` is a type alias for `IO ()`

**_NOTE_**: Unlike solution code, module declaration for the test fixture is optional.

## Pass/Fail methods

### shouldBe

```haskell
shouldBe :: (Eq a, Show a) => a -> a -> Expectation
```

The vast majority of the time, a test will simply require that a function output a specified value.

**Examples:**

```haskell
1 `shouldBe` 1 -- Will pass and display "Test Passed"

Nothing `shouldBe` Just "NOOOO"
-- expected: Just "NOOOO"
-- but got: Nothing
```

### shouldSatisfy

```haskell
shouldSatisfy :: Show a => a -> (a -> Bool) -> Expectation
```

`shouldSatisfy` asserts that some predicate holds for a given value.

**_NOTE_**: It is not a good considered good practice to write tests with `shouldSatisfy`, as the output is not generally informative. It is much better to use `shouldBe` instead.

**Examples:**

```haskell
"bar" `shouldSatisfy` (not . null) -- Will pass and display "Test Passed"

23 `shouldSatisfy` (> 42)  -- Will fail and display: "23 did not satisfy predicate!"
```

### shouldReturn

```haskell
shouldReturn :: (Eq a, Show a) => IO a -> a -> Expectation
```

`shouldReturn` asserts that an action returns a given value.

**Examples:**

```haskell
putStrLn "Haskell is awesome!" `shouldReturn` () -- Will pass and display "Test Passed"
```

### shouldThrow

```haskell
shouldThrow :: Exception e => IO a -> Selector e -> Expectation
```

`shouldThrow` asserts that an exception is thrown. The precise nature of that exception is described with a `Selector`.

**Examples:**

```haskell
error "foobar" `shouldThrow` anyException
```

A `Selector` is a predicate, it can simultaneously constrain the type and value of an exception.

```haskell
throw DivideByZero `shouldThrow` (== DivideByZero)
```

To select all exceptions of a given type, `const True` can be used.

```haskell
error "foobar" `shouldThrow` (const True :: Selector ErrorCall)
```

For convenience, predefined selectors for some standard exceptions are provided.

```haskell
error "foobar" `shouldThrow` anyErrorCall
```

Some exceptions (like `ErrorCall`) have no `Eq` instance, so checking for a specific value requires pattern matching.

```haskell
error "foobar" `shouldThrow` (\e -> case e of
    ErrorCall "foobar" -> True
    _ -> False
    )
```

For such exceptions, combinators that construct selectors are provided.
Each combinator corresponds to a constructor; it takes the same arguments,
and has the same name (but starting with a lower-case letter).

```haskell
error "foobar" `shouldThrow` errorCall "foobar"
```

### hidden

```haskell
data Hidden = Module String | FromModule String String
hidden :: [Hidden] -> Expectation
```

Allows the user to hide imported modules and functions from imported modules.
Useful for testing functions already implemented in other libraries.

**Examples:**

Suppose we wanted to write an exercise where the user has to reimplement `xor`.
We don't want them to use `xor` from `Data.Bit`, so we don't want the following code to pass.

```haskell
module Solution where
import qualified Data.Bit (xor)

xor :: Int -> Int
xor = Data.Bit.xor
```

If we add into the test suite

```haskell
hidden [Module "Data.Bit"]
```

Then the above code will fail, since it imports `Data.Bit`.

If we wanted to allow for the other functions in `Data.Bit` except `xor` and `and`, we could add to our test suite:

```haskell
hidden [FromModule "Data.Bit" "xor", FromModule "Data.Bit" "and"]
```

## QuickCheck

### Using QuickCheck with Hspec

You can use arbitrary QuickCheck properties with Hspec, but they must be of type `Property`.
QuickCheck's `property` function can be used to turn anything that is a member of the `Testable` class into a `Property`.

For more information, see the [QuickCheck Tutorial](http://www.haskell.org/haskellwiki/Introduction_to_QuickCheck2)

**Example:**

```haskell
import Test.Hspec
import Test.QuickCheck

main :: IO ()
main = hspec $ do
  describe "read" $ do
    context "when used with ints" $ do
      it "is inverse to show" $ property $
        \x -> (read . show) x == (x :: Int)
```

## HUnit

### Running a HUnit test suite with Hspec

Hspec's `fromHUnitTest` can be used can be used to run HUnit tests with Hspec.
Ordinary spec items and HUnit tests can be freely intermixed.

**Example:**

```haskell
import Test.Hspec
import Test.Hspec.HUnit (fromHUnitTest)
import Test.HUnit

main :: IO ()
main = hspec $ do
  describe "some ordinary spec items" $ do
    it "returns the first element of a list" $ do
      head [23 ..] `shouldBe` (23 :: Int)

  describe "some legacy HUnit tests" $ do
    fromHUnitTest testSuite

-- | A HUnit test suite
testSuite :: Test
testSuite = TestList [
    TestLabel "test_read_is_inverse_to_show" test_read_is_inverse_to_show
  , TestLabel "test_23_is_equal_to_42" test_23_is_equal_to_42
  ]

test_read_is_inverse_to_show :: Test
test_read_is_inverse_to_show = TestCase $ do
  (read . show) (23 :: Int) @?= (23 :: Int)

-- a failing test case
test_23_is_equal_to_42 :: Test
test_23_is_equal_to_42 = TestCase $ do
  23 @?= (42 :: Int)
```
