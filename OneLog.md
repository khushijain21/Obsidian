how about a logger module with below features?

1. support structured and unstructured logging
2. support to add extensions(extra key/value pairs in json structure)
3. integrated with lumberjack (for log rotation)
4. support for users to create custom log levels  apart from default ones (like TRACE, ALERT etc)
5. integration with syslog (can be standard or custom maintained with TLS support)
6. And all these things can configured using a config yaml (just like log4j.xml in case of java)
7. Support file logging


file:
	path: string
	logrotate: boolean

custom_log:
	name: string
	 level: string

extensions are supported 