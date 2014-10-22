# capistrano/jbundler

capistrano-jbundler is a small Capistrano 3 task which allows you to use [jbundler](https://github.com/mkristian/jbundler) to automatically
install jar dependencies declared in your [Jarfile](https://github.com/torquebox/maven-tools/wiki/Jarfile) during deploys.

## Installation

Add to the *top* of your gemfile:

    gem 'jbundler'

and then in your :development group, add:

    gem 'capistrano-jbundler'

And then execute:

    $ bundle

In your `Capfile`:

    require 'capistrano/jbundler'

And finally, in your JRuby application:

    JBUNDLER_CLASSPATH.each {|c| require c }

This will expose all Jarfile packages to your JRuby app.

## Usage

jbundler is automatically run after bundler. This causes it to install any dependent jars declared
in your Jarfile. It doesn't replace bundler due to jar-dependency version conflicts under recent
(Oct 2014) JRuby builds.

There are a number of settings you can set in your deploy.rb to override defaults. They are, with their defaults:

    set :jbundler_jarfile, -> { release_path.join('Jarfile') }
    set :jbundle_classpath, -> { release_path.join(".jbundler/classpath.rb") }
    set :jbundle_skip, nil
    set :jbundle_verbose, nil
    set :jbundle_local_repository, nil
    set :jbundle_settings, nil
    set :jbundle_offline, nil
    set :jbundle_proxy, nil
    set :jbundle_mirror, nil
    set :jbundle_work_dir, nil
    set :jbundle_vendor_dir, nil

## Contributing

1. Fork it ( https://github.com/[my-github-username]/capistrano-jbundler/fork )
2. Create your feature branch (`git checkout -b my-new-feature`)
3. Commit your changes (`git commit -am 'Add some feature'`)
4. Push to the branch (`git push origin my-new-feature`)
5. Create a new Pull Request
