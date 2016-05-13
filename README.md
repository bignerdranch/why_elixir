# Why Elixir and Phoenix?

**This is mainly meant to help us with sales**

Ruby and Rails is BNR's standard back end technology.
Why might we choose the Elixir language and/or the Phoenix framework instead?

One reason is that the software industry is moving to functional, concurrency-friendly languages.
BNR needs to be competent with languages like this, and Elixir has some unique properties that make it great for the web and flexible for other use cases.

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

> "Functional programming is associated with concurrency but it was not by design. It just happens that, by making the complex parts of our system explicit, solving more complicated issues like concurrency becomes much simpler." - [Jose Valim](http://www.sitepoint.com/an-interview-with-elixir-creator-jose-valim/)

### Performance

The Phoenix web framework is much more performant than Rails.
[One benchmark](https://github.com/mroth/phoenix-showdown/blob/master/README.md#benchmarking) showed Phoenix handling more than 10x the requests in a given period.
Phoenix was also much more consistent under load - Rails was more prone to have some requests bog down.

What's more, [Phoenix apps **without caching** drastically outperform Rails apps with caching](http://sorentwo.com/2016/02/02/caching-what-is-it-good-for.html).
This is important because caching is notorious for being a source of complexity and bugs, and because caching can't be used for moment-by-moment, personalized content like that offered by [Bleacher Report](http://bleacherreport.com/), which shows users news and tweets about the teams they're interested in and handles "five digits of requests per second", [according to a former senior developer there](http://www.elixirconf.eu/elixirconf2015/michael-schaefermeyer).

Better performance can also lead to simpler deployments and cost savings.

> "Bleacher Report is one of the best examples I've given, where they had a Ruby API and they rewrote it with Phoenix, and they were able to go from like, dozens of servers to two servers... and they only run two for redundancy."
>  --  Chris McCord [on Ruby Rogues](https://devchat.tv/ruby-rogues/253-rr-phoenix-and-rails-with-chris-mccord), 58:24

One of the ways Phoenix outperforms Rails is in faster, memory-efficient template rendering, based on how the Erlang VM handles string IO. [An Erlang web framework describes it this way](http://chicagoboss.org/about.htm):

> Erlang Respects Your RAM!
> Erlang is different from other platforms because when rendering a server-side template, it doesn't create a separate copy of a web page in memory for each connected client. Instead, it constructs pointers to the same pieces of immutable memory across multiple requests.
> So if two people request two different profile pages at the same time, they're actually sent the same chunks of memory for the header, footer, and other shared template snippets. The result is a server that can construct complex, uncached web pages for hundreds of users per second without breaking a sweat.
> With Erlang, you can run a website on a fraction of the hardware that Ruby and the JVM require, saving you money and operational headaches.

This strategy not only means less work for the Erlang VM, but less work for the operating system, as it can often [get those repeated header and footer strings from CPU cache instead of RAM](http://stackoverflow.com/questions/37167918/does-calling-writev-repeatedly-with-the-same-memory-address-allow-hardware-cac).

### Flexibility

The Phoenix framework has first-class support for realtime communication via websockets (or polling, as a fallback).
In benchmarks, the creators [have been able to serve 2 million simultaneously-connected clients](http://www.phoenixframework.org/blog/the-road-to-2-million-websocket-connections)!
Additionally, they already have native channel clients for iOS, Android, and C# (Windows devices).
With that kind of support, we can confidently build servers to support chat, networked games, and more.

Elixir is also a good candidate for running embedded code via [Nerves](http://nerves-project.org/).
This is not possible with standard Ruby (although it would be with [mruby](https://github.com/mruby/mruby)).

## Cons

- There are fewer libraries in Elixir than in Ruby, so we'd have more times when we have to write something ourselves. However:
  - We can use the many existing Erlang libraries
  - New Elixir libraries are being added quickly
  - Any remaining gaps are a chance for BNR to "make a name for ourselves" in Elixir by creating a great open source tool
- There are also fewer services for Elixir for things like error monitoring. However, this is also changing, and the Erlang VM provides much better tools by itself than Ruby does.
- We have less experience with Erlang and Phoenix than with Ruby and Rails. *This may mean there are downsides we don't know about yet*. However:
  - We already have developers using Elixir and contributing to Elixir projects
  - Phoenix applications are structured a lot like Rails apps, so the ramp-up time is much shorter for people familiar with Rails
  - We've already deployed a simple Phoenix app to Heroku successfully

## Indicators of a Good Fit

(Borrow from https://www.amberbit.com/blog/2015/12/22/when-choose-elixir-over-ruby-for-2016-projects/)

Really, any greenfield project that is a good fit for Rails is something we can do in Phoenix, as long as the client is willing to have us use it.

But we'd have an especially strong case if the project involves any or multiple of the following:

- System expecting high traffic or requiring very fast / consistent response times
- Minimal downtime is crucial
- Realtime updates (eg, stock ticker)
- Bidirectional realtime communication with websockets (eg, chat, games)
