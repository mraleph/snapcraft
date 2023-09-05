Architectures
=============

By default, Snapcraft builds a snap to run on the same architecture as the build
environment. This behaviour can be modified with the root keyword
``architectures`` in the snap’s ``snapcraft.yaml``.

How to create a snap for a specific architecture
------------------------------------------------

To create a snap that will be built on ``amd64`` and built for ``amd64``, use
one of the following ``snapcraft.yaml`` snippets.

core22
^^^^^^

For ``core22``::

  architectures:
    - build-on: amd64
      build-for: amd64

Building on ``amd64`` will produce 1 snap built for ``amd64``. Snapcraft will
raise an error when building on another architecture.

If ``build-for`` is omitted, then it will assume the value of ``build-on``. The
following snippet snippet will produce the same result::

  architectures:
    - build-on: amd64

The shorthand format will also produce the same result::

  architectures:
    - amd64

core20
^^^^^^

For ``core20``::

  architectures:
    - build-on: amd64
      run-on: amd64

Building on ``amd64`` will produce 1 snap built for ``amd64``. Snapcraft will
not raise an error when building on another architecture. Instead, it will
ignore the ``architectures`` keyword and build for the build-on architecture.

If ``run-on`` is omitted, then it will assume the value of ``build-on``. The
following snippet snippet will produce the same result::

  architectures:
    - build-on: amd64

The shorthand format will also produce the same result::

  architectures:
    - amd64

How to create a set of snaps for multiple architectures
-------------------------------------------------------

core22
^^^^^^

For ``core22``::

  architectures:
    - build-on: amd64
      build-for: amd64
    - build-on: arm64
      build-for: arm64

Building on ``amd64`` will produce 1 snap for ``amd64``. Building on ``arm64``
will produce 1 snap for ``arm64``. Snapcraft will raise an error when building
on another architecture.

If ``build-for`` is omitted, then it will assume the value of ``build-on``. The
following snippet snippet will produce the same result::

  architectures:
    - build-on: amd64
    - build-on: arm64

The shorthand format will also produce the same result::

  architectures:
    - amd64
    - arm64

core20
^^^^^^

For ``core20``::

  architectures:
    - build-on: amd64
      run-on: amd64
    - build-on: arm64
      run-on: arm64

Building on ``amd64`` will produce 1 snap built for ``amd64``. Building on
``arm64`` will produce 1 snap built for ``arm64``. Snapcraft will not raise
an error when building on another architecture. Instead, it will ignore the
``architectures`` keyword and build for the build-on architecture.

If ``run-on`` is omitted, then it will assume the value of ``build-on``. The
following snippet snippet will produce the same result::

  architectures:
    - build-on: amd64
    - build-on: arm64

The shorthand format will also produce the same result::

  architectures:
    - amd64
    - arm64

How to create an architecture independent snap
----------------------------------------------

core22
^^^^^^

For ``core22``::

  architectures:
    - build-on: amd64
      build-for: all

core20
^^^^^^

For ``core20``::

  architectures:
    - build-on: amd64
      run-on: all

How to create a cross-compiling snap
------------------------------------

core22
^^^^^^

For ``core22``::

  architectures:
    - build-on: amd64
      build-for: arm64

Building on ``amd64`` will produce 1 snap built for ``arm64``. Snapcraft will
raise an error when building on another architecture.

``core22`` can handle complex build plans::

  architectures:
    - build-on: amd64
      build-for: amd64
    - build-on: [amd64, arm64]
      build-for: arm64

Building on ``amd64`` will produce 2 snaps, 1 built for ``amd64`` and 1 built
for ``arm64``. Building on ``arm64`` will produce 1 snap built for ``arm64``.
Snapcraft will raise an error when building on another architecture.

core20
^^^^^^

For ``core20``::

  architectures:
    - build-on: amd64
      run-on: arm64

Building on ``amd64`` will produce 1 snap built for ``arm64``. Snapcraft will
not raise an error when building on another architecture. Instead, it will
ignore the ``architectures`` keyword and build for the build-on architecture.

Complex build plans like the previous ``core22`` example are not supported for
``core20``.

How to stage packages from another architecture
-----------------------------------------------

To use an ``i386`` package for an ``amd64`` snap, use the following
``snapcraft.yaml`` snippets for ``core22``::

  architectures:
    - build-on: amd64

  package-repositories:
    - type: apt
      formats: [deb]
      architectures: [i386]
      components: [main]
      suites: [jammy]
      key-id: F23C5A6CF475977595C89F51BA6932366A755776
      url: https://ppa.launchpadcontent.net/deadsnakes/ppa/ubuntu

  parts:
    mypart:
      stage-packages:
        - libpython3.11-minimal:i386
