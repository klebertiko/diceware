Wordlists
=========

The passphrases generated by `diceware` naturally depend on the set of
words used, the wordlists.

`diceware` comes with some wordlists out-of-the-box, that might be a
good choice for usual private use.

.. warning:: We do -- by default -- *not* use the `diceware standard
	     wordlist`_, but the `long EFF wordlist`_ (see below), because it is
         more secure and more comfortable to use.

	     But the "original" list is included in diceware as well
	     and you can pick it with the ``-w en_orig`` option.  You
	     *should* pick it when you use real dice as source of
	     randomness.

Currently we provide the following lists:

- `en_securedrop` (8192 words)

  We provide a hand-crafted `en_securedrop` wordlist provided
  by `@Heartsucker`_. It contains 8,192 english words and
  phrases. This list is based on the `diceware standard wordlist`_ and
  extended to offer better memorizable words. Please see
  https://github.com/heartsucker/diceware for details. The name
  `en_securedrop` refers to the `securedrop`_ project.

- `en` (8192 words)

  Apart from it we also provide the so-called `8k wordlist`_ from
  Mr. Reinhold as published on http://diceware.com/. It also contains
  8,192 english words and phrases and is something like the canonical
  wordlist for use with binary-geared entities like computers or
  nerds.

- `en_eff` (7776 words, default)

  This is the `long EFF wordlist`_ as published by the `Electronic Frontier
  Foundation`_ in mid-2016 and used by default. They put real `scientific
  effort`_ into the creation of this list which might considerably ease the
  use of passphrases generated with it. When using real dice (or other
  six-based randomness generators) use is definitely recommended!

  Please note, that this is currently the only list, that provides the
  `prefix property`_. That means it contains no word which is a prefix
  of another word. Lists without this property might provide a slightly
  decreased entropy.

- `en_orig` (7776 words)

  This is the `diceware standard wordlist`_ as provided by
  Mr. Reinhold. Something like the canonical list in former times,
  there are now considerable alternatives.

You can pick another list with the ``-w`` or ``--wordlist`` option.


Add Own Wordlists
-----------------

You can use any wordlist you like. Simply give the filename and it
will be used::

  $ diceware mywordlist.txt
  HiHelloHelloHiHiHi

You can even pipe-in dynamic wordlists. Just use the dash ``-`` as
filename::

  $ cat mywordgenerator.sh | diceware -
  HiHiHelloHiHiHello

for instance.

Of course you have to give the filenames of your files with each call
to `diceware`.

But, if you want to store a wordlist persistently, you can do so too.

The wordlists we offer for use with `diceware` are all stored in a
single folder. The exact location is output by ``--help`` at the very
end::

  $ diceware --help
  ...
  Wordlists are stored in /some/path/to/folder

Just put your own wordlists into this folder (here:
``/some/path/to/folder``) and rename the file to something like
``wordlist_MY_SPECIAL_NAME.txt``. Afterwards you can pick your
wordlist by running::

  $ diceware -w MY_SPECIAL_NAME

`diceware` will use this file of yours then to create a
passphrase. Please note that `diceware` only accepts files that are
named like::

  wordlist_NAME.txt

or::

  wordlist_OTHER_NAME.asc

I.e. we expect ``wordlist_`` at the beginning and some filename
extension like ``.txt`` at the end. Furthermore names must not contain
funny characters. In fact we accept regular letters, dashes, numbers,
and underscores only. Files that do not follow these naming convention
are ignored.

A list of all available wordlist names can also be retrieved with
``--help``. See the ``--wordlist`` explanation.


Plain Wordlists
---------------

Out of the box, `diceware` supports plain wordlists, PGP-signed
wordlists, and numbered wordlists. Plain wordlists look like this::

  termone
  termtwo
  anotherterm

Each line in such a file is considered a word of the wordlist. Empty
lines are ignored.

Whitespaces are allowed if they are not at the beginning or end of a
line, stripped off otherwise.


Numbered Wordlists
------------------

Numbered wordlists contain numbers in each line, telling a
sequence of dice rolls like so::

  11111    aterm
  11112    anotherterm
  ...

`diceware` detects such lines and in this case extracts ``aterm`` and
``anotherterm`` as wordlist entries.

Apart from simple digits written next to each other, `diceware` also
accepts numbers separated by dashes like this::

  1-1-1-1-1   aterm
  1-1-1-1-2   anotherterm

which is handy when working with wordlists for dice with more than 9
sides.


PGP-signed Wordlists
--------------------

PGP-signed wordlists are wordlists (ordinary or numbered ones), that
have been cryptographically signed with PGP or GPG. They look like
this::

  -----BEGIN PGP SIGNED MESSAGE-----
  Hash: SHA512

  foo
  bar
  baz

  -----BEGIN PGP SIGNATURE-----
  Version: GnuPG v1

  iJwEAQEKAAYFAlW00GEACgkQ+5ktCoLaPzSutwP8DVgdjBFqRXNKaZlvd8pR+P3k
  8xx5XLC0OFwZQFx4Ls8xl3+/xfvCNxCGSZjD6BGPzNZCK7bmQQYWcrsoEyX5jAC3
  dXjAPj0nct/PkJQlrUjUI2qrO0dFfU7sRj0Gn9TOlQQkKoQVwy7pY/6HaScGNepL
  J8BNUPYdOWeVgxY1jSY=
  =WXfu
  -----END PGP SIGNATURE-----

and are normally stored with the ``.asc`` filename extension. Signed
wordlists can be verified to detect changes, although this is not
automatically done by `diceware`.

.. warning:: Diceware does *not* automatically verify PGP-signed
             files.


.. _`8k wordlist`: http://world.std.com/~reinhold/diceware8k.txt
.. _`diceware standard wordlist`: http://world.std.com/~reinhold/diceware.wordlist.asc
.. _`Electronic Frontier Foundation`: https://eff.org/
.. _`@Heartsucker`: https://github.com/heartsucker/
.. _`long EFF wordlist`: https://www.eff.org/files/2016/07/18/eff_large_wordlist.txt
.. _`prefix property`: https://en.wikipedia.org/wiki/Prefix_code
.. _`scientific effort`: https://www.eff.org/deeplinks/2016/07/new-wordlists-random-passphrases
.. _`securedrop`: https://github.com/freedomofpress/securedrop
