# Why Elixir and Phoenix?

**This is mainly meant to help us with sales**

Ruby and Rails is BNR's standard back end technology.
Why might we choose the Elixir language and/or the Phoenix framework instead?

## Pros

### Reliability

First off: yes, Elixir is a fairly new language.
That might make you think it's not reliable.
But Elixir is mostly a friendly interface to the Erlang virtual machine.

Erlang has been used [since the 80s](http://www.erlang.org/course/history) to build some of the most reliable systems in the world.
It was developed to run telephone systems.
People die if the telephone doesn't work.

So the creators of Erlang developed a language and baked into it strategies for running a complex system with [almost no downtime](http://stackoverflow.com/questions/8426897/erlangs-99-9999999-nine-nines-reliability).
Those strategies include having multiple levels of "supervising" processes in a system to reboot parts that have errors.
They were doing microservices before microservices were cool.

And because they were running their code on many telephone switches, they also invented a great model for running code concurrently (see below).

New as it is, Elixir harnesses all the power of Erlang and provides friendly syntax and tools for using it.

### Concurrency

Computer CPUs are no longer getting dramatically faster each year.
Instead, we get machines with more cores.
This lets our code run faster, but **only if it can run concurrently** - meaning, different bits of code run simultaneously on different cores.

The main problem with concurrent code is having two pieces of code mess with the same data at the same time, creating unexpected results.
Object-oriented languages like Ruby don't provide great tools for avoiding such problems.
But functional languages, like Elixir, do.
Writing concurrent code in Elixir is extremely easy, and it's nearly impossible to accidentally interfere with other code that's running at the time.

In Ruby, we never ask "can I create another object?"
Everything in Ruby is an object, and objects are cheap.
We create as many as we want.

In Elixir, processes are like objects - we can create thousands of them, all running concurrently, and never worry about it.
This ability simplifies a lot of the problems we normally have in Ruby.

### Simplicity

When we write Rails applications, our Rails app depends on a lot of other pieces.

We can only handle one web request at a time with a Rails app, and we can't spin up new processes as needed, so we have to use tools to spawn multiple application servers up front and put a web server like Nginx in front of them to hand off requests.

We can't do slow background tasks without blocking our web requests, so we have to add Redis and Resque to take care of running background jobs.

We can't use a precious process to maintain a websocket connection with a user, so we have to add Pusher to get realtime functionality.

We can't keep a big Ruby process running all the time to do scheduled tasks, so we add a dependency on `cron`.

In Elixir, we can spin up a nearly limitless number of processes as needed, so we can (in theory) forego all those tools.

Elixir code is also simpler to understand than object-oriented code because it has explicitness as a value.

    "Functional programming is associated with concurrency but it was not by design. It just happens that, by making the complex parts of our system explicit, solving more complicated issues like concurrency becomes much simpler." - [Jose Valim](http://www.sitepoint.com/an-interview-with-elixir-creator-jose-valim/)

### Performance

The Phoenix web framework is much more performant than Rails, handling more than 10x the requests in a given period [by one benchmark](https://github.com/mroth/phoenix-showdown/blob/master/README.md#benchmarking).
Phoenix was also much more consistent under load - Rails was more prone to have some requests bog down.

Better performance can also lead to simpler deployments and cost savings.

    "Bleacher Report is one of the best examples I've given, where they had a Ruby API and they rewrote it with Phoenix, and they were able to go from like, dozens of servers to two servers, and they're running, like, you know, tens of millions of users per month... and they only run two for redundancy."
    Chris McCord [on Ruby Rogues](https://devchat.tv/ruby-rogues/253-rr-phoenix-and-rails-with-chris-mccord), 58:24

McCord said that they achieved this despite removing a lot of caching from their code.
Caching is notorious for being hard to deal with, so that's a double win.

(To watch later: http://www.elixirconf.eu/elixirconf2015/michael-schaefermeyer)

### Flexibility

(Possible to do [embedded stuff](http://nerves-project.org/) with Elixir, Ruby not so much unless you use [mruby](https://github.com/mruby/mruby))

## Cons

- Fewer libraries than Ruby == more often have to reinvent the wheel
  - But we can use any Erlang libraries
  - New libraries being added quickly
  - More chances for BNR to make open source contributions
  - 🤔 this is actually secretly a huge pro for us, because given the saturation of Ruby it's been hard to get a foot in on the OSS world (other than random contributions). It'd be _awesome_ to own something as a team/company.
- There are fewer experienced Elixir devs for hire (by us or our clients) than Ruby devs
  - However, lots of devs are looking for Elixir jobs, so hiring might be easier
- We are inexperienced with Erlang / Phoenix
   - This means there may be downsides we don't know about yet

## Indicators of a Good Fit
https://www.amberbit.com/blog/2015/12/22/when-choose-elixir-over-ruby-for-2016-projects/

Any / multiple of the following:

- Greenfield project
- System expecting high traffic or requiring very fast / consistent response times
- Minimal downtime is crucial
- Realtime updates (eg, stock ticker)
- Bidirectional realtime communication with websockets (eg, chat, games)
- 🤔 also worth mentioning that perhaps any project that would work for Rails would also work with Elixir/Phoenix and might even be stronger.
- 🤔 another indicator might be as simple as the client is willing to have deliverables written in elixir
