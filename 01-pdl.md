---
layout: page
title: Programming with Perl
subtitle: Analyzing Patient Data
minutes: 30
---
> ## Learning Objectives {.objectives}
>
> *   Explain what a library is, and what libraries are used for.
> *   Load a Perl library and use the things it contains.
> *   Read tabular data from a file into a program.
> *   Assign values to variables.
> *   Select individual values and subsections from data.
> *   Perform operations on arrays of data.
> *   Display simple graphs.

Words are useful,
but what's more useful are the sentences and stories we build with them.
Similarly,
while a lot of powerful tools are built into languages like Perl,
even more live in the **libraries** they are used to build.

In order to load our inflammation data,
we need to **import** a library called PDL (short for Perl Data Language).
In general you should use this library if you want to do fancy things with numbers,
especially if you have matrices.
We can load PDL using:

~~~ {.perl}
use strict;    # FIXME: see <https://github.com/zmughal/perl-novice-inflammation/issues/2>
use warnings;
use PDL;
~~~

Importing a library is like getting a piece of lab equipment out of a storage locker
and setting it up on the bench.
Once it's done,
we can ask the library to read our data file for us:

~~~ {.perl}
PDL->rcols( 'inflammation-01.csv', [], colsep => ',' );
~~~
~~~ {.output}
[
 [ 0  0  …  0  0]
 [ ⋮  ⋮  ⋱  ⋮  ⋮]
 [ 0  0  …  2  1]
 [ 0  1  …  0  0]
]
~~~

The expression `rcols( ... )` is a **function call** that asks Perl to run the
function `rcols` that belongs to the `PDL` library. The **arrow notation** is
used in Perl to refer to parts of things `thing->component`.

The call to to `rcols` has three **parameters**:
the name of the file we want to read,
a list of the columns to read,
and the **delimiter** that separates values on a line. 
These both need to be character strings (or **strings** for short),
so we put them in quotes.

When we are finished typing and press `Enter` (or `Return`),
the interpreter runs our command.
Since we haven't told it to do anything else with the function's output,
the interpreter displays it.
In this case,
that output is the data we just loaded.

Our call to `numpy.loadtxt` read our file,
but didn't save the data in memory.
To do that,
we need to **assign** the array to a **variable**.
A variable is just a name for a value,
such as `x`, `current_temperature`, or `subject_id`.
Python's variables must begin with a letter.
We can create a new variable simply by assigning a value to it using `=`.
As an illustration,
let's step back and instead of considering a table of data,
consider the simplest "collection" of data,
a single value.
The line below assigns a value to a variable:

~~~ {.perl}
my $weight_kg = 55;
~~~

Once a variable has a value, we can print it:

~~~ {.perl}
print $weight_kg, "\n"; # FIXME: should this be say()?
~~~
~~~ {.output}
55
~~~

and do arithmetic with it:

~~~ {.perl}
print 'weight in pounds: ', 2.2 * $weight_kg, "\n"; # FIXME: say()?
~~~
~~~ {.output}
weight in pounds: 121.0
~~~

We can also change a variable's value by assigning it a new one:

~~~ {.perl}
$weight_kg = 57.5;
print 'weight in kilograms is now:', $weight_kg;
~~~
~~~ {.output}
weight in kilograms is now: 57.5
~~~

FIXME note that we don't need to put a `my` since we aren't declaring it for the first time.

As the example above shows,
we can print several things at once by separating them with commas.

If we imagine the variable as a sticky note with a name written on it,
assignment is like putting the sticky note on a particular value:

