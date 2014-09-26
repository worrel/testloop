# TestLoop
[![Gitter](https://badges.gitter.im/Join Chat.svg)](https://gitter.im/worrel/testloop?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge)

TestLoop is a library that provides an automated execution and
reloading of a cabal's test-suites whenever a haskell file is
modified.

NOTE: To get started quickly check the project in the examples folder.

## Usage

Once you have a test suite using a haskell test library ([hspec][hspec], [HUnit][hunit],
[test-framework][testframe], etc), write the following in your project's cabal file:

```cabal
test-suite tests
  type: exitcode-stdio-1.0
  hs-source-dirs: src, test
  main-is: TestSuite.hs
  -- configuration for your testsuite here

executable testloop
  main-is: TestLoop.hs
  -- all your project sources (+tests) directores
  hs-source-dirs: src, test
  build-depends:
    base             == 4.6.*,
    -- your project + test dependencies
    testloop         == 0.1.*
```

And in the `test/TestLoop.hs` file:

```haskell
module Main where

import System.TestLoop (setupTestLoop)

main :: IO ()
main = setupTestLoop
```

Install and run your TestLoop, as soon as you start editing your
source files it will automatically compile and run your tests, instant
feedback FTW.

Note: Currently TestLoop expects you to have your tests in a `test` folder

[hspec]: http://hspec.github.io/
[hunit]: http://hunit.sourceforge.net/HUnit-1.0/Guide.html
[testframe]: http://batterseapower.github.io/test-framework