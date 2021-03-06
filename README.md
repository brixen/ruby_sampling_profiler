# Ruby Randomized Sampling Profiler

[![Build Status](https://travis-ci.org/brixen/ruby_sampling_profiler.svg?branch=master)](https://travis-ci.org/brixen/ruby_sampling_profiler)

The patches here implement modifications to Ruby's source code to add a
randomized sampling profiler.

## Supported Versions

The subdirectories contain the patch file for that version of Ruby.

## Controlling The Sampler

The profiler is enabled by setting the `RUBY_PROFILER` environmental variable.
The value is not significant.

The sampling "tick" value defaults to 5 milliseconds and can be set in
nanoseconds by setting `RUBY_PROFILER_TICK`. The value cannot be set to less
than 5 milliseconds.

The profiler can emit data about its functioning. Set the
`RUBY_PROFILER_STATS` value to the name of a file. The file is formatted as a
CSV with the following columns:

    PID, sample, random, random_percent, delta_sec, delta_nsec, delta_nsec_percent

1. PID - this enables distinguishing parent from child process stats
1. sample - the sample index
1. random - the random delta to the sample interval
1. random_percent - the percentage of the sample interval represented by the
   random delta
1. delta_sec - the delta between the value of the second set for the interval
   and the measured second when the sampler thread wakes up
1. delta_nsec - the delta between the value of the nanosecond set for the
   interval and the measured nanosecond when the sampler thread wakes up
1. delta_nsec_percent - the percentage of the sample interval represented by
   the delta_nsec.

## Building

### Using ruby-install

For information about using `ruby-install`, see [the ruby-install
docs](https://github.com/postmodern/ruby-install)

    $ ruby-install -p https://raw.githubusercontent.com/brixen/ruby_sampling_profiler/master/ruby-2.1/profiler.diff ruby 2.1.10

### Using ruby-build

For information about using `rbenv` and `ruby-build`, see [the ruby-build
docs](https://github.com/rbenv/ruby-build).

    $ rbenv install --patch 2.1.10 < <(curl -sSL https://raw.githubusercontent.com/brixen/ruby_sampling_profiler/master/ruby-2.1/profiler.diff)

### Using RVM

For information about using `rvm`, see [the RVM
docs](https://rvm.io/rubies/patching).

    $ rvm install 2.1.10 --patch https://raw.githubusercontent.com/brixen/ruby_sampling_profiler/master/ruby-2.1/profiler.diff

## References

1. [Evaluating the Accuracy of Java Profilers](https://plv.colorado.edu/papers/mytkowicz-pldi10.pdf)
1. [Statistically Rigorous Java Performance Evaluation](https://dri.es/files/oopsla07-georges.pdf)

## License

See LICENSE
