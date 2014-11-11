---
layout: post
title:  "Semantic Grids with Bourbon and Neat"
date:   2014-11-10 02:26:00
categories: Sass Grid
---

[Neat](http://neat.bourbon.io/) is a grid framework maintained by the [Thoughtbot](http://thoughtbot.com/) team. It is built on top of [Bourbon](http://bourbon.io/), a library for [Sass](http://sass-lang.com/), maintained also by the people at [Thoughtbot](http://thoughtbot.com/). It can be installed to work with [Compass](http://compass-style.org/) as well, but maybe you need to update your Compass version to 1.0.0 or newer. Previous releases of Compass do not support Sass 3.3 which is needed if you want to install the current version of the Bourbon gem. With that in mind, you might want to check which version is installed in your machine, before installing or updating any ruby gem. Just type `$ compass version` from the command line and the output should contain which version of the Compass gem you are running.  

<dl>

  <dt>Not found</dt>
  <dd>
    If the command returned a not found argument, you don't need to install Compass at all to work with Bourbon. I'm not going to do it myself in this case, so apart from the configuration and installation of the compatible Ruby gems, I won't cover any other aspect of the Compass workflow. And I must admit also that I do not see many reasons to combine these two frameworks. One of the greatest avantages I've found when working with Bourbon over Compass is the unobtrusive control and freedom that the framework provides you over your own project. It doesn't tie you to floating positioned layouts, or any other kind of inmutable approach for building your site. However and apart from the fact that I find myself most confortable when using a set of tools instead of another, I am aware that Compass is, and has been for some time, the framework employed for the deployment of Sass preprocessed stylesheets, that has gathered the widest support among the developer's community. This gives me a slight idea of the volume of projects that might be runnig older versions of Sass.
  </dd>

  <dt>Compass 1.0.0</dt>
  <dd>
    Back to the output returned after entering `$ compass version`; if you are running 1.0.0 or newer you are safe to go and install the Bourbon gem. 
  </dd>

  <dt>Older Compass (needed for this project)</dt>
  <dd>
    If you need to run Bourbon with an older version of Compass or Sass you need to install bourbon 3.2.x. So instead of just typing `$ gem install bourbon` which defaults to the latest stable release you can specify a version as in `$ gem install bourbon -v 3.2.3` . In the case of Neat the release thet is compatible with Sass 3.2 is neat 1.5.1 `$ gem install neat -v 1.5.1` . Bitters can be installed normally `$ gem install bitters` since it is compatible with versions of Sass starting from Sass 3.0.0.

    <ul>
      <li><a href="https://github.com/thoughtbot/bourbon#requirements">Bourbon</a></li>
      <li><a href="https://github.com/thoughtbot/neat#requirements">Neat</a></li>
      <li><a href="https://github.com/thoughtbot/bitters#requirements">Bitters</a></li>
    </ul>
  </dd>

  <dt>Older Compass (needed for different projects)</dt>
  <dd>
    Otherwise if the previous command returned Compass 0.12.6 or similar, chances are that you might still need to run older Compass projects which require Compass 0.12.6 and Sass 3.2. If this is the case but you still update your installation, you won't notice any incompatibility issue untill you run an older Compass project on Sass 3.3, which will prompt you with constant deprecation warnings and syntax errors.

    When collaborating on projects that require a group of people to work on the same files and track them with some kind of version control system this is a common problem. [Bundler](http://bundler.io/) is a tool that helps solving ruby dependencies. It can be installed as a Ruby gem `$ gem install bundle` and works in a similar way as other package management systems. If you want to specify a set of gems for a specific project by running `$ bundle init` in the root directory of the project will create a Gemfile where you can declare the necessary dependencies:

<pre>
  <code class="gemspec">
  gem 'compass', '~>1.0.0'
  gem 'sass'
  gem 'bourbon'
  gem 'neat'
  gem 'bitters'
  </code>
</pre>

    This file works in Ruby in a similar way the packaje.json works inside a Node.js project. As in a Node.js project running `$ npm install` would launch the node package manager (npm) to start the installation of the dependencies especified in the package.json; with Bundle you'd have to run `$ bundle install`. This will launch the installer and solve any conflicts when matching your global Ruby installation to your local especification. Once the installation has completed you'll find a new file Gemfile.lock that contains a complete reference to the installation performed by bundle. 
  </dd>
</dl>

<!--<pre>
  <code class="gemspec">
    GEM
      remote: https://rubygems.org/
      specs:
        bitters (0.10.1)
          bourbon (>= 3.2)
          sass (>= 3.2)
          thor
        bourbon (4.0.2)
          sass (~> 3.3)
          thor
        chunky_png (1.3.3)
        compass (1.0.1)
          chunky_png (~> 1.2)
          compass-core (~> 1.0.1)
          compass-import-once (~> 1.0.5)
          rb-fsevent (>= 0.9.3)
          rb-inotify (>= 0.9)
          sass (>= 3.3.13, < 3.5)
        compass-core (1.0.1)
          multi_json (~> 1.0)
          sass (>= 3.3.0, < 3.5)
        compass-import-once (1.0.5)
          sass (>= 3.2, < 3.5)
          ffi (1.9.6)
        multi_json (1.10.1)
          neat (1.7.0)
          bourbon (>= 4.0)
        sass (>= 3.3)
        rb-fsevent (0.9.4)
        rb-inotify (0.9.5)
          ffi (>= 0.5.0)
        sass (3.4.7)
      thor (0.19.1)

  PLATFORMS
    ruby

  DEPENDENCIES
    bitters
    bourbon
    compass (~> 1.0.0)
    neat
    sass


  </code>
</pre>-->


The last thing to comment in relation to Compass is that when installed with bundle, to be sure that you are running the correct Compass version, you should run `$ bundle exec compass watch` instead of `$ compass watch`. 

To start using the Bourbon stack of tools just go to your _sass directory and run `$ bourbon install` , `$ neat install` and `$ bitters install`. Each of these three commands will create a folder containing the source files. It is important that you don't make any modifications to these files. They contain the default parameters used by each of these tools, but since the variables are declared with the following sass syntax:

    $variable-option: value !default; 

The !default termination means that if the variable has no value assigned, it should default to the one especified here. So keeping these three folders untouched will keep you from having to commit them to a repository. Since bundle has created a Gemfile.lock with the specific versions your project is running, anyone wanting to clone the project will only have to run `$ bundle install` at the root of the project, then move to the folder containing the Sass files and run `$ bourbon install` , `$ neat install` and `$ bitters install` to start working on the project, at any state of its development. 


