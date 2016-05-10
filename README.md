# UNURAN

[UNU.RAN](http://statmath.wu.ac.at/unuran/index.html) is a universal random number generator.
It's exactly what you want for discrete event simulation.
There are still choices to make, so read the book listed at the end.

## Installation

UNU.RAN isn't on yum or apt or brew, so BinDeps isn't a great help
here. If you want to install it with the
option to use RngStreams, then you would ensure that it is configured
to create shared libraries and that those shared libraries use PIC:

    tar zxf rngstreams-1.0.1.tar.gz
    cd rngstreams-1.0.1
    ./configure --with-pic --enable-shared
    make
    sudo make install
    tar zxf unuran-1.8.1.tar.gz
    ./configure --with-pic --enable-shared --with-urng-rngstream --with-urng-default=rngstream
    make
    sudo make install

Then ensure those libraries are in the LD_LIBRARY_PATH, perhaps by
using "locate libunurand" or "mdfind -name libunurand" to find them
and then running:

    export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/usr/local/lib

substituting the appropriate directory for your installation.

After that, `Pkg.install("UNURAN")`, and you should be running.


## Documentation

Read the [documentation at UNU.RAN](http://statmath.wu.ac.at/software/unuran/doc/unuran.html).
This wrapper for Julia is as thin as tissue paper, but it seems to do
all the things, including passing in your own distribution function.
Look at Julia's docs on [calling C code](http://docs.julialang.org/en/release-0.4/manual/calling-c-and-fortran-code/)
to see how to write your own probability distribution function.
It was created with
Clang, using the `gen2.jl` script. The wrapping for Julia isn't well
tested, but we can be guaranteed that the distributions will work correctly,
and that's what keeps me up at night.

## Rights and Privileges

Anybody who cares about random number generation enough to 
use UNU.RAN can be part of this repo. I mean, how bad could you be?
Send me a note. If I'm horribly busy, I'll at least give you access.

## References

Hörmann, Wolfgang, Josef Leydold, and Gerhard Derflinger. Automatic nonuniform random variate generation. Springer Science & Business Media, 2013.
This is the group that wrote UNU.RAN.

Luc, Devroye. "[Non-uniform random variate generation.](http://www.nrbook.com/devroye/)" NY: Springer (1986). This is awesome.


[![Build Status](https://travis-ci.org/adolgert/UNURAN.jl.svg?branch=master)](https://travis-ci.org/adolgert/UNURAN.jl)
