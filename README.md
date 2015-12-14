Table of Contents
=================

<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->


- [Dependencies](#dependencies)
- [Patches](#patches)
- [I. Adding the named-configs-prototype layer to your build](#i-adding-the-named-configs-prototype-layer-to-your-build)
- [II. Usage](#ii-usage)
- [III. Limitations](#iii-limitations)
- [IV. TODO](#iv-todo)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

This layer holds a prototype of a BBCLASSEXTEND-based approach to recipe
variants whose only difference is configuration (e.g. normal and minimal
busybox variants).

Dependencies
============

This layer depends on:

  URI: git://git.openembedded.org/bitbake
  branch: master

  URI: git://git.openembedded.org/openembedded-core
  layers: meta
  branch: master


Patches
=======

Please submit any patches via github's pull requests mechanism, and open
issues in github's issue tracker to report any problems.

I. Adding the named-configs-prototype layer to your build
=========================================================

In order to use this layer, you need to make the build system aware of
it:

    $ bitbake-layers add-layer /path/to/meta-named-configs-prototype

II. Usage
=========

To add a configuration variant for a specific recipe, in a bbappend:

    BBCLASSEXTEND += "named-configs:variant-name"

Then adjust the configuration (e.g. custom entry in filespath to override
a file, or PACKAGECONFIG, or whatever) as appropriate for the variant, using
either the virtclass or pn-based override. Ex:

    BBCLASSEXTEND += "named-configs:minimal"
    PACKAGECONFIG_virtclass-named-config-minimal = ""

III. Limitations
================

Since the variants are per-recipe, not global, there's currently no way to
automatically propogate any PREFERRED_VERSION_<recipe> to also apply to the
variants, the way it's done for multilibs.

IV. TODO
========

- [ ] Consider adding RPROVIDES/RCONFLICTS/RREPLACES of the original binary
  package names to all the binary packages, ideally also including dynamic, so
  selection could be handled on target as well as at build time.
