# Why Elixir and Phoenix?

**This is mainly meant to help us with sales**

Ruby and Rails is BNR's standard back end technology.
Why might we choose the Elixir language and/or the Phoenix framework instead?

## Pros

### Reliability

(Elixir seems new, but Erlang VM actually old, history of reliability, supervision trees, etc)
http://stackoverflow.com/questions/8426897/erlangs-99-9999999-nine-nines-reliability

### Concurrency

(CPUs not getting faster anymore, this is how we do performance now...)

🤔 and despite its improvements over the years, ruby is still not great at this. It will probably always be harder with OOP

### Simplicity

"Functional programming is associated with concurrency but it was not by design. It just happens that, by making the complex parts of our system explicit, solving more complicated issues like concurrency becomes much simpler." - [Jose Valim](http://www.sitepoint.com/an-interview-with-elixir-creator-jose-valim/)
(Phoenix framework has similar philosophy)

(Since processes are cheap, you don't need Redis + Resque for bg jobs, or Pusher for realtime stuff, or cron jobs for scheduled stuff, or RabbitMQ for pub-sub... you can just use Elixir processes)

### Performance

Phoenix is [much more performant than Rails](https://github.com/mroth/phoenix-showdown/blob/master/README.md#benchmarking).
[One benchmark on Heroku](http://www.littlelines.com/blog/2014/07/08/elixir-vs-ruby-showdown-phoenix-vs-rails/) showed Phoenix handling 8.94 times more traffic than Rails with 3.74x less CPU usage.
Phoenix was also much more consistent under load - Rails was more prone to have some requests bog down.

- Better performance can also lead to simplicity and cost savings
  - (On [Ruby Rogues](https://devchat.tv/ruby-rogues/253-rr-phoenix-and-rails-with-chris-mccord) (58:24) McCord gave anecdote of people moving from Rails to Phoenix and needing far fewer servers) around 58min in
  - 2 million active connections on Phoenix
  - "Bleacher Report is one of the best examples I've given, where they had a Ruby API and they rewrote it with Phoenix, and they were able to go from like, dozens of servers to two servers, and they're running, like, you know, tens of millions of users per month, and they were able to reduce down to a couple of servers, and they only run two for redundancy. So they could get away with running their entire platform on one Phoenix server... the whole idea of the database being the bottleneck I think isn't actually true because they were able to go from the same Postgres database that they were using heavy caching on the Ruby side, they removed all caching and they just talk directly to the database from the Phoenix side, and they were able to reduce dozens of servers down to just one or two."
  🤔 WHOA

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
