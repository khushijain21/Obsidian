
This blog is intended for beginners to get started with SwiftLog. Logs provide easy and quick observability into your applications

SwiftLog is the standard Logging library developed by Apple and the sections below aim to introduce its use cases.

#### Log a simple message - 

```swift
import Logging

let logger = Logger(label: "app-identifier")

logger.info("Hello World!")
```

The available log levels are `.trace`, `.debug`, `.info`, `.notice`, `.warning`, `.error`, and `.critical`. For example, to set the logging level to `.debug`:

```swift
logger.logLevel = .debug
```

The log messages will only output if their level is equal to or higher than the configured logging level. 

#### Logging with Metadata - 

You can additional context to your log message using metadata

```swift
import Logging

// Create a logger
var logger = Logger(label: "com.example.MyLogger")

// Log a message with metadata
logger.info("user logged in", metadata: ["user-id": "\(user.id)"])
```

You can also (similarly) set metadata on your logger to log your context with each message. Setting metadata on your logger can be useful when you would like to differentiate logs from various sources.  

```swift
// Define metadata
var metadata = Logger.Metadata()
metadata["requestID"] = "12345"
metadata["userID"] = 42

// Set metadata on the logger 
logger.metadata = metadata
```

#### Setting your logger with custom `logHandler`:

A `logHandler` is the backend implementation of the logger which decides how/where your log messages should be outputted. There are various logHandler available by SwiftLog like `MultiplexLogHandler`, `StreamLogHandler`, `SwiftLogNoOpLogHandler`.  More [here](https://apple.github.io/swift-log/docs/current/Logging/Structs/MultiplexLogHandler.html)

For example: `StreamLoghandler` directs your log message to stderr/stdout and `MultiplexLogHandler` can be used send to your log messages to multiple handlers. This provides end user with great flexibility.

1. You can set a `logHandler` on your logger as below:

```swift
import Logging

// Create a logger
var logger = Logger(label: "com.example.MyLogger")

// Create a StreamLogHandler for logging to standard output (console)
let streamLogHandler = StreamLogHandler.standardOutput(label: "com.example.MyLogger"

// Set a custom log handler on the logger
logger.logHandler = streamlogHandler

// Log some messages
logger.info("This is an info message")
logger.error("This is an error message")
```

2. You can also set up a LogginSystem for your application

>`LoggingSystem` is set up just once in a given program to set up the desired logging backend implementation. 

```swift
import Logging

LoggingSystem.bootstrap(MyLogHandler.init) // your LogHandler might have a different bootstrapping step
var logger1 = Logger(label: "first logger")
logger1.logLevel = .debug
var logger2 = logger1
logger2.logLevel = .error  
```

where both `logger1` and `logger2` have the same `logHandler`
`

