FocusList
=========

[![Build Status](https://secure.travis-ci.org/cdepillabout/focuslist.svg)](http://travis-ci.org/cdepillabout/focuslist)
[![Hackage](https://img.shields.io/hackage/v/focuslist.svg)](https://hackage.haskell.org/package/focuslist)
[![Stackage LTS](http://stackage.org/package/focuslist/badge/lts)](http://stackage.org/lts/package/focuslist)
[![Stackage Nightly](http://stackage.org/package/focuslist/badge/nightly)](http://stackage.org/nightly/package/focuslist)
[![BSD3 license](https://img.shields.io/badge/license-BSD3-blue.svg)](./LICENSE)

A `FocusList` is a sequence of elements which has one element as its `Focus`. It
supports quick insertion and indexing by its implementation with
[`Seq`](http://hackage.haskell.org/package/containers-0.6.0.1/docs/Data-Sequence.html#t:Seq).

## Example

Here is a short example of using `FocusList`.

```haskell
module Main where

import Data.FocusList
  ( Focus(Focus), FocusList, appendFL, fromListFL, getFocusItemFL, prependFL
  , singletonFL
  )
import Data.Foldable (toList)

-- | Create a new 'FocusList' from a list.  You must set the 'Focus' of the new
-- 'FocusList'.  The 'Focus' is counting from zero, so the @goat@ element should
-- have the 'Focus'.
--
-- If you try to specify a 'Focus' out of range from the input list,
-- 'fromListFL' will return 'Nothing'.
myFocusList :: Maybe (FocusList String)
myFocusList = fromListFL (Focus 2) ["hello", "bye", "goat", "dog"]

-- | You can get the focused element from an existing 'FocusList'
--
-- If the 'FocusList' is empty, this returns 'Nothing'.
myFocusElement :: FocusList String -> Maybe String
myFocusElement focuslist = getFocusItemFL focuslist

-- | You can append to either side of a 'FocusList'.
--
-- 'singletonFL' creates a 'FocusList' with a single element.
-- That single element will have the 'Focus'.
--
-- 'myFocusListAppended' will have a value of
-- @FocusList (Focus 1) ["bye", "hello", "foobar"]@
myFocusListAppended :: FocusList String
myFocusListAppended =
  prependFL "bye" (appendFL (singletonFL "hello") "foobar")

-- | 'FocusList' is an instance of 'Functor' and 'Foldable', so you can use
-- functions like 'fmap' and 'toList' on a 'FocusList'.
fmapAndConvertToList :: FocusList Int -> [String]
fmapAndConvertToList focuslist = toList (fmap show focuslist)

main :: IO ()
main = do
  putStrLn "myFocusList:"
  print myFocusList

  putStrLn "\nmyFocusListAppended:"
  print myFocusListAppended

  putStrLn "\nmyFocusElement myFocusListAppended:"
  print (myFocusElement myFocusListAppended)

  putStrLn "\nfmap length myFocusListAppended:"
  print (fmap length myFocusListAppended)

  putStrLn "\nfmapAndConvertToList (fmap length myFocusListAppended):"
  print (fmapAndConvertToList (fmap length myFocusListAppended))
```

## Maintainers

- [Grendel-GrendelGrendel](https://github.com/Grendel-Grendel-Grendel)
- [cdepillabout](https://github.com/cdepillabout)
