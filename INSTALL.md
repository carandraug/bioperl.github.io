---
title: "INSTALL"
layout: default
---

BIOPERL INSTALLATION

The following are instructions for installing BioPerl on
Unix, Linux, and Mac OS X. Windows installation instructions can be
found in [INSTALL.WIN](INSTALL.WIN.html).

LINUX PACKAGE MANAGERS

Many Linux distributions have already packaged bioperl.  Installing
from their package managers is the preferred and easiest method to
install bioperl, even if their version is a bit out of date.

If your distribution does not package bioperl, or if for some reason
you prefer to install it from source, then continue reading.

SYSTEM REQUIREMENTS

 * `Perl 5.6.1 or higher` Version 5.8 or higher is highly
   recommended. Modules are tested against version 5.8 and
   above.
 * `make` For Mac OS X, this requires installing the Xcode Developer
   Tools.


PRELIMINARY PREPARATION

These are optional, but regardless of your subsequent choice of
installation method, it will help to carry out the following steps.
They will increase the likelihood of installation success
(especially of the optional dependencies).

* Upgrade CPAN:

```
perl -MCPAN -e shell
```

* Install or upgrade `Module::Build`, and make it your preferred installer:

```
cpan>install Module::Build
cpan>o conf prefer_installer MB
cpan>o conf commit
```

* Install the *expat* library by whatever method is appropriate for your system (e.g. `apt`, `yum`, `homebrew`).


INSTALLING BIOPERL THE EASY WAY USING CPAN

We highly recommend using
[cpanminus](https://metacpan.org/pod/distribution/App-cpanminus/bin/cpanm) for
installing BioPerl and its dependencies. We also highly recommend (if possible)
using a tool like [perlbrew](https://perlbrew.pl) to locally install a modern
version of perl (a version that is higher than perl 5.16).  The linked
pages describe how to install each tool; make sure if you install perlbrew that
you follow up with installing `cpanm`:

```
perlbrew install-cpanm
```

Then, you can install BioPerl:

```
cpanm Bio::Perl
```

You can also use the CPAN shell to install BioPerl. For example:

```
perl -MCPAN -e shell
```

Or you might have the `cpan` alias installed:

```
cpan
```

Then find the name of the latest BioPerl package:

```
cpan>d /bioperl/

 ....

 Distribution    C/CJ/CJFIELDS/BioPerl-1.007001.tar.gz
 Distribution    C/CJ/CJFIELDS/BioPerl-1.007001.tar.gz
 Distribution    C/CJ/CJFIELDS/BioPerl-1.007001.tar.gz
```

And install the most recent:

```
cpan>install C/CJ/CJFIELDS/BioPerl-1.007001.tar.gz
```

If you've installed everything perfectly and all the network
connections are working then you will pass all the tests run in the
`./Build test` phase. Sometimes you may see a failed test. Remember that
there are over 900 modules in BioPerl and the test suite is running more
than 12000 individual tests, a failed test may not affect your usage
of BioPerl.

If there's a failed test and you think that the failed test will not
affect how you intend to use BioPerl then do:

```
cpan>force install C/CJ/CJFIELDS/BioPerl-1.007001.tar.gz
```

If you're concerned about a failed test and need assistance or advice
then contact bioperl-l@bioperl.org, and provide us the detailed
results of the failed install.


INSTALLING BIOPERL FROM GITHUB

The very latest version of Bioperl is at github.com. If you want this
version then download it from https://github.com/bioperl/bioperl-live
as a *zip file, or retrieve it using the command line:

```
git clone https://github.com/bioperl/bioperl-live.git
cd bioperl-live
```

If you've downloaded the *zip file then unzip that and cd to the
BioPerl directory.

Issue the build commands:

```
perl Build.PL
```

You will be asked a few questions about installing BioPerl scripts
and running various test suites, hit *return* to accept the defaults.

Test:

```
./Build test
```

Install:

```
./Build install
```

You may need root permissions in order to run `./Build install`, so you
will want to talk to your systems manager if you don't have the necessary
privileges. Or you can install the package in your own home
directory, see INSTALLING BIOPERL USING local::lib.


INSTALLING BIOPERL USING local::lib

If you lack permission to install Perl modules into the standard
system directories you can install them in your home directory
using `local::lib`. The instructions for first installing
`local::lib` are found here:

https://metacpan.org/pod/local::lib

Once `local::lib` is installed you can install BioPerl using a
command like this:

```
perl -MCPAN -Mlocal::lib -e 'CPAN::install(C/CJ/CJFIELDS/BioPerl-1.6.924.tar.gz)'
```

INSTALLING BIOPERL SCRIPTS

BioPerl comes with a set of production-quality scripts that are
kept in the scripts/ directory. You can install these scripts if you'd
like, simply answer the questions during `perl Build.PL`.
The installation directory can be specified by:

```
perl Build.PL
./Build install --install_path script=/foo/scripts
```

By default they install to */usr/bin* or similar, depending on platform.


THE TEST SYSTEM

The BioPerl test system is located in the *t/* directory and is
automatically run whenever you execute the `./Build test` command.

The tests have been organized into groups
based upon the specific task or class the module being tested belongs
to. If you want to investigate the behavior of a specific test such as
the Seq test you would type:

```
./Build test --test_files t/Seq/Seq.t --verbose
```

The `--test_files` argument can be used multiple times to try a set of test
scripts in one go. The `--verbose` arguement outputs the detailed test results, instead of just the summary you see during `./Build test`.

The `--test-files` argument can also work as a glob. For instance, to
run tests on all SearchIO modules, use the following:

```
./Build test --test_files t/SearchIO* --verbose
```

If you are trying to learn how to use a module, often the test suite
is a good place to look. All good extreme programmers try and write a
test BEFORE they write the module to insure that their module behaves
the way they expect. You'll notice some `ok` and `skip` commands in a
test, this is part of the Perl test suite that signifies a passed test
with an 'ok N', where N is the test number. Alternatively you can tell
Perl to skip tests. This is useful when, for example, your test
detects that the network is not present and thus should skip, not
fail, any tests that require a network connection.

The core developers have indicated that future releases of BioPerl
will require that new modules come with a test suite with some minimal
tests.  Modules that lack adequate tests or could otherwise be
considered 'unstable' will be moved into a separate developer
distribution until adequate tests are added and the API stablizes.
