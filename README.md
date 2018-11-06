### shoryuken
---
https://github.com/phstc/shoryuken

```
gem 'shuryuken'
gem 'aws-sdk-sqs'
bundle

bundle exec shoryuken sqs create hello
bundle exec shoryuken -q hello -r ./hello_worker.rb

bundle exec shoryuken sqs create hello
bundle exec shoryuken -q hello -R

```

```
class HelloWorker
  include Shoryuken::Worker
  shoryuken_options queue: 'hello', auto_delete: true
  def perform(sqs_msg, name)
    puts "Hello, #{name}"
  end
end

HelloWorker.perform_async('Ken')

# app/jobs/hello_job.rb
class HelloJob < ActiveJob::Base
  queue_as 'hello'
  def perform(name)
    puts "Hello, #{name}"
  end
end

# config/application.rb
module YourApp
  class Application < Rails::Application
    config.active_job.queue_adapter = :shoryuken
  end
end

Hello.perform_later('Ken')

```

```
```


