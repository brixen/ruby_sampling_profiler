# Ruby Randomized Sampling Profiler

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

    $ ruby-install -p https://raw.githubusercontent.com/brixen/ruby_sampling_profiler/master/ruby-2.1/profiler.diff ruby 2.1.10

### Using ruby-build

    $ TODO

### Using RVM

    $ TODO

# License

See LICENSE
