---
title: "How Many Zope Repositories Are Compatible With Pypy?"
date: 2021-04-19T11:38:06+02:00
tags:
- zope
- all-repos
- pypy
---

Today, Johannes Raggam asked on the [Plone/Zope community forum](https://community.plone.org/t/zope-plone-on-pypy/13726)
whether [Zope](https://github.com/zopefoundation/Zope) is able to run on [PyPy](https://www.pypy.org/).

While I am not entirely sure,
and I have some vague memories about potential problems with `RestrictedPython`,
I can certainly grep the almost 300 Zope repositories for signs of `PyPy` support.

The best sign of `PyPy` support is IMHO that we run tests for it :-)

In order to grep in all repositories I use [all-repos](https://github.com/asottile/all-repos) written by Anthony Sottile.

A naive attempt would something like this...

```bash
❯ all-repos-grep -C all-repos-zope.json "pypy" -- 'tox.ini'
output_zope/zopefoundation/Acquisition:tox.ini:   pypy,
output_zope/zopefoundation/Acquisition:tox.ini:   pypy3,
output_zope/zopefoundation/AuthEncoding:tox.ini:    pypy
output_zope/zopefoundation/AuthEncoding:tox.ini:    pypy3
```

This should be pretty self-explanatory.
- grep
- in all Zope repos
- for pypy
- but only in tox.ini files

The problem is... there is also pypy3, so I get double hits.

As I am only interested in the repositories,
and not in the configuration itself,
a better way to grep is...

```bash
❯ all-repos-grep -C all-repos-zope.json "pypy" --repos-with-matches -- 'tox.ini'
output_zope/zopefoundation/Acquisition
output_zope/zopefoundation/AuthEncoding
output_zope/zopefoundation/BTrees
output_zope/zopefoundation/DateTime
output_zope/zopefoundation/ExtensionClass
output_zope/zopefoundation/Missing
output_zope/zopefoundation/MultiMapping
output_zope/zopefoundation/Persistence
...
```

When I pipe the result to `wc -l` I get the number of repositories... 200!

I am pretty surprised that so many repositories support `PyPy`!

In order to judge this number,
let's see how many active repositories are there in total?

```bash
❯ all-repos-list-repos -C all-repos-zope.json | wc -l
287
```
