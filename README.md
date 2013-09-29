Just Run Phing
================

Inspired by Beau Simensen`s work on just-run-phpunit this project should allow
PHP developers to just type naked `phing` wherever they are but actually
executing `vendor/bin/phing` for projects that have Phing required via Composer
and falling back to a globally installed version of Phing if not. Kudos to Beau
Simensen for this idea!


Installation
------------

The `just-run-phing` file in the bash directory must be sourced in some way.
This can be done manually during an interactive session or it can be done by
sourcing it in `.profile`, `.bash_profile`, `.bashrc`, or some other means.
This seems to vary greatly depending on the distro so this exercise is left up
to the user to decide the best way to get this accomplished.

Assuming that `.bashrc` is processed on every login, you would add the following
to `.bashrc`:

    # Source the Bash specific instance of just-run-phing
    . ~/workspaces/just-run-ping/bash/just-run-phing


Usage
-----

In all cases, this utility relies on the `PHING_PATH` environment variable. It
contains a list of `:` separated paths similar to the `PATH` environment
variable. Each path will be checked for an executable file called `phing`. The
first time this file is found it will be executed and the return value of the
execution is returned.

The `PATH` is queried last to determine if a globaly installed version of
Phing is available.

If you need to extend the search path (say you regularly have Composer's vendor
bin redirected somewhere non-standard like `vendor-bins`) you can prepend or
append it to `PHING_PATH`. For example:

    export PHING_PATH="${PHING_PATH}:vendor-bins"

This will ensure that `vendor-bins` will be checked after the other default
paths have been checked.