
https://gist.github.com/kaylareopelle/76079747c1a7528449670b8bd1c78893  - gist to use ruby's built in logger with Otel instrumentation

https://newrelic.com/sites/default/files/2022-03/melt-101-four-essential-telemetry-data-types.pdf  - newrelic

https://ruby.github.io/play-ruby/ - Ruby playground

https://medium.com/@micosmin/learn-tdd-in-ruby-in-5-easy-steps-3ab28014fec4  - tests in ruby

- Official Ruby docs - https://try.ruby-lang.org/
https://betterstack.com/community/guides/logging/how-to-view-and-configure-ruby-logs/ - ruby inbuilt logger

https://docs.ruby-lang.org/en/master/Logger.html#method-i-format_message - Ruby logger documentation

https://github.com/open-telemetry/opentelemetry-ruby/tree/main/sdk  - Opentelemetry ruby sdk

https://logger.rocketjob.io/customize.html - semantic logging docs

https://www.rubyguides.com/2016/02/ruby-procs-and-lambdas/ - Ruby procs and lambdas

https://codex.org/2022/08/19/setting-up-ruby-wsl2.html  - install ruby in wsl

https://rubyhero.dev/mixins-prepend-extend-include#heading-include - prepend, extend and include in Ruby

https://rubocop.org/ - rubocop linter

https://www.alchemists.io/articles/ruby_method_parameters_and_arguments/
https://www.rubyguides.com/2018/06/rubys-method-arguments/ - ruby method argument


I couldn't find any blog posts, so I asked a few of my colleagues about why Ruby uses namespacing so heavily, and this is what they shared:  

- Namespacing provides an easy way to see relationships between classes in their names and allows individual modules/classes to have specific domains. It also provides a parallel between the location of the class in the file tree and the class's name, but there isn't any technical requirement to do so. It's more of a best practice/preference by developers.
- Modules/Classes can also be declared with less nesting in a more compact form. This isn't the style that the dominant linter, Rubocop, recommends. The logger patch could be rewritten as:

```
class OpenTelemetry::Instrumentation::Logger::Patches::Logger
end 
# content ...
end 
```
  ``
- For Go, there's definitely namespacing involved but it's possibly more spread out. Go relies on `.mod` files to declare module namespacing and then relies on directory structure to accomplish nested package names within a module. Furthermore, it's a best practice in Go to try to do 1 module per project. So from that perspective, Ruby's ability to put multiple modules in the same project, using any directory structure the developer wants (though we try to match nested namespacing as a practice), and not using dedicated module files could certainly make all of the boilerplate at the top of an `.rb` file more verbose for sure.

I hope this helps!