Architectures
=============

Build-on, build-for, and run-on
-------------------------------

``core22`` uses ``build-on`` and ``build-for``. ``core20`` uses ``build-on``
and ``run-on``.

build-on
^^^^^^^^

The architecture of the machine that the snap is built on (the machine where
Snapcraft runs).

build-for
^^^^^^^^^

The architecture of the machine that the snap is built for (the machine where
the snap will be installed).

run-on
^^^^^^

This is used for ``core20`` and has the same meaning as ``build-for``. It has
been replaced with the preferred term ``build-for`` in ``core22``.

Build plans
-----------

A build plan is a list of what snaps snapcraft will build. It can be defined
in the ``snapcraft.yaml`` and filtered with command-line arguments and
environment variables.

core22
^^^^^^

Snapcraft can create multiple snaps, each built for a different architecture.
Consider the following ``snapcraft.yaml`` snippet::

  architectures:
    - build-on: amd64
      build-for: amd64
    - build-on: [amd64, arm64]
      build-for: arm64

If snapcraft executes on an ``amd64`` machine, then it will create the
following build plan::

  - on amd64 build for amd64
  - on amd64 build for arm64

2 snap files will be created, ``my-snap_1.0_amd64.snap`` and
``my-snap_1.0_arm64.snap``.

This build plan can be filtered with the environment variable
``SNAPCRAFT_BUILD_FOR=<arch>`` or the command-line argument
``--build-for=<arch>``. The command-line argument takes priority over the
environment variable. In the example above, using ``--build-for=arm64`` would
cause snapcraft to only build 1 snap for ``arm64``.

core20
^^^^^^

Build plans are not supported in ``core20`` so building a ``core20`` snap will
only produce 1 snap.

Build plans in destructive mode
-------------------------------
todo: describe how multiple builds will occur in destructive mode

Architecture errors
-------------------
todo: describe common architecture errors
(like the same arch in multiple build-on's for core20)
