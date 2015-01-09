# lein-test-refresh

This is a Leiningen plug-in that automatically refreshes and then runs
your `clojure.test` tests when a file in your project changes

## Features

- Allows you to have a quick feedback cycle by automatically
  refreshing your code and running your tests.
- Runs previously failing tests first, giving you feedback even quicker.
- Can pass result of running your tests to a notification command of your
  choice.
- Has built in Growl notification support.
- Can be configured to only notify you on failures.
- [Supports](https://github.com/jakemcc/lein-test-refresh/blob/master/CHANGES.md#040) subset of Leiningen test selectors.
- Times how long it takes to run your tests.

## Usage

![Latest version](https://clojars.org/com.jakemccrary/lein-test-refresh/latest-version.svg)

Add the above to your `~/.lein/profiles.clj`. It should look similar to below.

    {:user {:plugins [[com.jakemccrary/lein-test-refresh "0.5.5"]]}}

Alternatively you may add it to your `project.clj`.

    (defproject sample
      :dependencies [[org.clojure/clojure "1.6.0"]]
      :profiles {:dev {:plugins [[com.jakemccrary/lein-test-refresh "0.5.5"]]}})

Enter your project's root directory and run `lein test-refresh`. The
output will look something like this.

    $ lein test-refresh
    *********************************************
    *************** Running tests ***************

    <standard clojure.test output>
    
    Failed 1 of 215 assertions
    Finished at 08:25:20.619 (run time: 9.691s)
    
Your terminal will just stay like that. Fairly often `lein-test-refresh`
polls the file system to see if anything has changed. When there is a
change your code is tested again.

If you need to rerun your tests without changing a file then hit
`Enter` when focused on a running `lein test-refresh`.

## Notifications

`lein-test-refresh` supports specifying a notification command. This
command is passed a short message after your tests have run. This
command is configured through your `project.clj` or `profiles.clj`.
For example, if you want to send OSX notifications using
[terminal-notifier](https://github.com/alloy/terminal-notifier) then
you would add the following to your `project.clj` or `profiles.clj`

    :test-refresh {:notify-command ["terminal-notifier" "-title" "Tests" "-message"]} 

`lein-test-refresh` also has built-in Growl support. To receive Growl
notifications run `lein test-refresh :growl`. This has been tested
with modern versions of Growl for [OS X](http://growl.info/),
[Linux](http://mattn.github.com/growl-for-linux/), and
[Windows](http://growlforwindows.com/). You can also always set this
to true by setting `:test-refresh {:growl true}}`. An example can be
found in the [sample.project.clj](sample.project.clj).

`:notify-on-success` is another available option. It can be used to
turn off notifications when your tests are successful. Set
`:notify-on-success false` to turn off success notifications. An
example can be found in the [sample.project.clj](sample.project.clj).

### Latest version & Change log

The latest version is the highest non-snapshot version found in
[CHANGES.md](CHANGES.md) or whatever the below images says (sometimes
image doesn't seem to load).

![Latest version](https://clojars.org/com.jakemccrary/lein-test-refresh/latest-version.svg)

### Leiningen 1.0

This project has not been tested with versions of Leiningen 1. This
project is heavily based of `lein-autoexpect` which has been tested
against Leiningen 1. I would expect this project to work as well but
I'm not going to bother testing it nor do I plan on supporting it.

## Compatibility

lein-test-refresh has been tested to work with Clojure 1.5.1 and 1.6
with Leiningen 2.3+.

Because of
[tools.namespace](https://github.com/clojure/tools.namespace) changes
`lein-test-refresh` requires that your project use Clojure >= 1.3.0. If
your project also depends on a version of `tools.namespace` < 0.2.1
you may see occasional exceptions.

## License

Copyright (C) 2011-2015 [Jake McCrary](http://jakemccrary.com)

Distributed under the Eclipse Public License, the same as Clojure.


