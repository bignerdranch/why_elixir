# Why Elixir and Phoenix?

**This is mainly meant to help us with sales**

Ruby and Rails is BNR's standard back end technology.
Why might we choose the Elixir language and/or the Phoenix framework instead?

## Pros

### Reliability

(Elixir seems new, but Erlang VM actually old, history of reliability, supervision trees, etc)

### Concurrency

(CPUs not getting faster anymore, this is how we do performance now...)

### Simplicity

"Functional programming is associated with concurrency but it was not by design. It just happens that, by making the complex parts of our system explicit, solving more complicated issues like concurrency becomes much simpler." - [Jose Valim](http://www.sitepoint.com/an-interview-with-elixir-creator-jose-valim/)
(Phoenix framework has similar philosophy)

(Since processes are cheap, you don't need Redis + Resque for bg jobs, or Pusher for realtime stuff, or cron jobs for scheduled stuff...)

### Performance

Phoenix is much more performant than Rails.
[One benchmark on Heroku](http://www.littlelines.com/blog/2014/07/08/elixir-vs-ruby-showdown-phoenix-vs-rails/) showed Phoenix handling 8.94 times more traffic than Rails with 3.74x less CPU usage.
Phoenix was also much more consistent under load - Rails was more prone to have some requests bog down.

### Flexibility

(Possible to do [embedded stuff](http://nerves-project.org/) with Elixir, Ruby not so much unless you use [mruby](https://github.com/mruby/mruby))

## Cons

- Fewer libraries than Ruby == more often have to reinvent the wheel
  - But we can use any Erlang libraries
  - New libraries being added quickly
  - More chances for BNR to make open source contributions
- There are fewer experienced Elixir devs for hire (by us or our clients) than Ruby devs
  - However, lots of devs are looking for Elixir jobs, so hiring might be easier
- We are inexperienced with Erlang / Phoenix
   - This means there may be downsides we don't know about yet

## Indicators of a Good Fit

- Greenfield project
