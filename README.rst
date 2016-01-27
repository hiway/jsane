JSane
=====

JSane is a JSON "parser" that makes attribute accesses easier.


Motivation
----------

Picture the scene. You're a jet-setting developer who is obsessed with
going to the gym. One day, a world-class jewel thief kidnaps you and
asks you to hack into the super-secure bank server in thirty seconds,
while an ultramodel is performing oral sex on you. You hurriedly trace
the protocol on the wire, only to discover, to your dismay, that it uses
JSON. Nested JSON, with levels and levels of keys.

It's hopeless! You'll never type all those brackets and quotation marks
in time! Suddenly, a flash of a memory races through your mind, like
some cliche from a badly-written Github README. You launch the shell and
type two words::

    import jsane

The day is saved.


Motivation (non-Hollywood version)
----------------------------------

Are you frustrated with having to traverse your nested JSON key by key?

::

    root = my_json.get("root")
    if root is None:
        return None

    key1 = root.get("key1")
    if key1 is None:
        return None

    key2 = key1.get("key2")
    if key2 is None:
        return None

    <five more times>

Is your code ruined by pesky all-catching ``except`` blocks?

::

    try:
        my_json["root"]["key1"]["key2"]["key3"]
    except:
        return None

Are you tired of typing all the braces and quotes all the time?

::

    my_json["root"]["key1"[""]][]"]']'"}}""]

Now there's JSane!


Motivation (non-infomercial version)
------------------------------------

Okay seriously, ``this["thing"]["is"]["no"]["fun"]``. JSane lets you
``traverse.json.like.this``. That's it.


Usage
-----

Using JSane is simple, at least. It's pretty much a copy of the builtin `json`
module. Here's an example::

    >>> import jsane

    >>> j = jsane.loads('{"some": "json"}')
    >>> j.some
    "json"

If the key does not exist, you'll get an exception. You can get rid of that by
specifying a default::

    >>> import jsane

    >>> j = jsane.loads('{"some": "json"}')
    >>> j(default="💩").haha_sucka_this_doesnt_exist
    "💩"


Due to Python being a non-insane language, there's a limit to the amount of
crap you can pull with it, so JSane actually returns a `Traversable`  object if
you access a `dict` or `list`::

    >>> j = jsane.loads('{"foo": {"bar": "baz"}}')
    >>> type(j.foo)
    Traversable

If you want your object back, call `.resolve()`::

    >>> j.foo.resolve()
    {"bar": "baz"}

That's about it. I'm not loving this API, so if anyone has any good
recommendations on how I may better fulfil my unholy purpose, I'm changing the
API on the spot. No guarantees of stability before version 1, as always. Semver
giveth, and semver taketh away.

Help needed/welcome/etc, mostly with designing the API. Also, if you find this
library useless, let me know.


License
-------

BSD. Or MIT. Whatever's in the LICENSE file. I forget. It's permissive, though,
so relax.


Self-promotion
--------------

It's me, Stavros.


FAQ
---

* Do you find it ironic that the README for JSane is insane?

  No.

* Is this library awesome?

  Yes.