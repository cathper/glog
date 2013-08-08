Binary search
=============

I happened to think of "Programming Pearls" statement that "90 % of programmers
cannot write binary search correctly". Not a quote; find the book and read. This
is not the point though. I thought about binary search.

Usually input is described to be a "sorted array". I noticed that different
implementations can give different results but still be correct.

Is that common knowledge to anyone who have ever been introduced to binary
search? I simply haven't thought of it before (or I have forgot). I have even
taught binary search---shame on me. I challenge you to figure out why and how
before you continue reading.

Consider the following a hint:

    Input:
        A sorted array.
        An item to search for.

    Output:
        The position of the item in the sorted array or ``-1`` if the item is
        not present.


This is why (by example)
------------------------

The hint is wrong by several means. Firstly, is ``a[i] <= a[i+i]`` or is ``a[i]
>= a[i+1]``?

Secondly, "The" does not make sense unless ``a[i] < a[i+1]``; or, "sorted array"
should be "sorted strictly increasing array". (If "increasing" is supposed to
mean "non-decreasing" or "strictly increasing" is a matter of convention that
two programmers may choose differently. So to avoid confusion, I prefer to write
"strictly (de|in)creasing" or "non-(de|in)creasing".)

Oh, and by the way, the array could be of any "orderable" stuff, so I would
prefer to have a comparison operator as input. Anyway, we focus on integers
where ``a[i] <= a[i+1]`` since that is what I expect you expect when you read
"sorted array".

Setting the scene: Assume 0-indexed arrays. I will only use strict comparisons.
I will always have item to search for to the left of the comparison and test for
truths.

The pairs of rounding and comparison are (a) ``(floor, >)`` and (b) ``(ceil,
<)``. (Doodle until you agree.)

The example: Search for ``1`` in ``[1,1]``.

If you choose (a) you return ``0``. If you choose (b) you return ``1``.


Binary search as it should be
-----------------------------

Was that sufficient provocative? I'll continue along that path.

This is how you should define the input and output:

    Input:
        ``a``: Array of integers sorted non-decreasingly.
        ``x``: integer to search for.
    Output:
        The smallest index ``s`` in ``a`` such that ``a[s] = x`` or ``-1`` if
        ``x`` is not present in ``a``.


(Go generalize. Hints: "ascending", "integers", "smallest", "total order",
"finite", "upper set" and probably others.)

This is how you should program it for (a).

.. code-block:: ruby

    def binary_search(array, x)
      left  = 0
      right = array.length-1
      
      while true
        middle = (left + right)/2 # Implicit flooring.
        # middle means "middle skewed to the left".
        # middle is -1 if a = []. Therefore I prefer (a).
        
        break unless left < right
        
        if x > array[middle]
          left = middle+1
        else
          right = middle
        end
      end

      return x == array[middle] ? middle : -1
    end

Did I prefer an imperative solution in Ruby? No, but I suspect fewer would
carefully read my Haskell code. Also, I preferred a "non-out-of-bound-checking"
version.

I am sure you cannot write it more elegant. Now you want to try, right? I hope
so.


Notice
------

The probability that I got all this right is at most 10 %. Pull requests are
welcome.

Have fun_. I haven't, yet.

.. _fun: https://en.wikipedia.org/wiki/Binary_search_algorithm
