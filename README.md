spdx-license-match
==================

Suppose you work with open source and want to package a project for a
distribution. The project’s license looks like it might be the MIT License, but
you’re not sure which variant of it. (Or is it BSD? You could never tell them
apart.) But you really need the license’s [SPDX] identifier for your
distribution package…

This small tool helps you in finding out which open source license variant
you’re dealing with.

[SPDX]: https://spdx.org/licenses/

Installation
------------

After clong the Git repository, update the submodule:

    git submodule update --init

Then you can symlink the script `spdx-license-match` to any directory in your
`$PATH` and use it as-is.

Usage
-----

Suppose you have a project with the following license:

    $ cat LICENSE
	Copyright (C) 2017 Roland Hieber <r.hieber@pengutronix.de>

	Permission is hereby granted to use, copy, modify, and/or distribute this
	software for any purpose with or without fee.

	THE SOFTWARE IS PROVIDED "AS IS" AND THE AUTHOR DISCLAIMS ALL WARRANTIES
	WITH REGARD TO THIS SOFTWARE INCLUDING ALL IMPLIED WARRANTIES OF
	MERCHANTABILITY AND FITNESS. IN NO EVENT SHALL THE AUTHOR BE LIABLE FOR
	ANY SPECIAL, DIRECT, INDIRECT, OR CONSEQUENTIAL DAMAGES OR ANY DAMAGES
	WHATSOEVER RESULTING FROM LOSS OF USE, DATA OR PROFITS, WHETHER IN AN
	ACTION OF CONTRACT, NEGLIGENCE OR OTHER TORTIOUS ACTION, ARISING OUT OF
	OR IN CONNECTION WITH THE USE OR PERFORMANCE OF THIS SOFTWARE.

What do you think, which of the countless open source licenses is this?
Take a guess :-)

	$ spdx-license-match --guess MIT --short -n 3 LICENSE
	Match: 27% MIT-feh
	Note: match for MIT-feh is pretty bad. Maybe try a better --guess.
	Match: 29% MIT
	Note: match for MIT is pretty bad. Maybe try a better --guess.
	Match: 42% MIT-CMU
	Note: match for MIT-CMU is pretty bad. Maybe try a better --guess.

The top match has only 42% common words. Hmm, doesn’t seem to be MIT… let’s
try all licenses, and let’s also see the differences between our input and the
top match:

	$ spdx-license-match LICENSE
	Match: 91% 0BSD
	Diff:
	  --- 0BSD.txt
	  +++ input
	  
	  @@ -1,7 +1,7 @@
	  Copyright (C) [-2006 by Rob Landley <rob@landley.net>-] {+2017 Roland Hieber 
	  <rohieb@rohieb.name>+}
	  
	  Permission {+is hereby granted+} to use, copy, modify, and/or distribute this  
	  software for any purpose with or without [-fee is hereby granted.-] {+fee.+}
	  
	  THE SOFTWARE IS PROVIDED "AS IS" AND THE AUTHOR DISCLAIMS ALL WARRANTIES WITH  
	  REGARD TO THIS SOFTWARE INCLUDING ALL IMPLIED WARRANTIES OF MERCHANTABILITY 

OK, a different copyright holder and some words are in a different order, it’s
good enough to be described as the 0BSD license.

For more options, see `spdx-license-match --help`.

License
-------

spdx-license-match is itself licensed under the 0BSD license, see the output
above or the file LICENSE in this repository.
