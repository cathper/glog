I hate the concept of time
==========================

Think of how nice it would be if time wasn't around. You wouldn't be late. "I
did that tomorrow" would make as much sense as "Why isn't it done?".

No, really. The odds of getting things wrong when you are mingling with time are
against you.

* How do you handle time zones in your programming language of choice?
* Is DST (Daylight Saving Time) handled in your application?
* What about leap seconds?
* What happens in your application if time goes backwards?

If you agree, just enjoy http://www.youtube.com/watch?v=jHPOzQzk9Qo#t=107s
s/Life/Time/ whereas you may watch this guy first to agree
http://www.youtube.com/watch?v=-5wpm-gesOY.


Use a library
-------------

The odds that some random library maintainer got it right over time is hopefully
larger than the odds that you will in first shot. Do not build your own unless
you really know what you are doing. (Is this about cryptography?)

I went to http://tzinfo.github.io and wrote

.. code-block:: ruby

    require 'tzinfo'
    TZInfo::Timezone.get('Europe/Copenhagen').now

which returned "2013-10-21 11:41:57 UTC".

.. role:: ruby(code)
   :language: ruby

Wait. It returned a :ruby:`Time` object. With current time in UTC? (That would
be the same as :ruby:`Time.now.utc`.) No. With local time (in the given time
zone), but with time zone set to UTC. So, local time is UTC? No. Copenhagen is
CET/CEST.

What the fsck?

So, I get a :ruby:`Time` object where the "time" is right, but the time zone is
wrong.

That is actually the intended behaviour, but just shows how much care you must
take.

Dear Time, you are a trouble maker.

