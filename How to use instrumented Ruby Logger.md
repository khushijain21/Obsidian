### Scenario 1: Basic Usage
Default config
```ruby
require_relative 'path/to/your/logger_patches_file.rb'

logger = Logger.new
logger.extend(OpenTelemetry::Instrumentation::Logger::Patches::Logger)
logger.initialize

```