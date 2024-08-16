


I was a  contributor to projects like Grafana, Beyla and Victoria Metrics. I assumed a mentorship program like LFX would help me make bigger, more impactful contributions. OpenTelemetry is one of the most active repositories under the CNCF which aims to provide a uniform observability format—a massive ambition that has seen great ongoing success.

### Initial Challenges
The aim of the program was to provide at least one logging bridge per language which would help end-users start using OTLP logging natively. The initial challenges were understanding the project's architecture, design patterns, and reading a lot of code! Each language's logging bridge needed to integrate seamlessly.

### Technical Contributions and Highlights

1. **Zap Logger Integration**: One of the significant contributions I made was integrating the `zap` logger with OpenTelemetry. `zap` is a widely used high-performance logging library for Go, known for its efficiency and speed. 
   
   While significant progress has been made, some PR's are still under review, aiming to finalize this integration. Quick shoutout to @AmirBlum @RobertPajak and @TylerYahn for providing feedback, reviewing code and brainstorming different approaches together.
2. **Ruby's Default Logger**: I also worked on integrating OpenTelemetry with Ruby's default logger. This involved creating middleware that automatically injects trace context into log entries, making it easier for developers to correlate logs with traces. 
 
   Thankful to @KaylaReopella for helping me ramp up to Ruby. Similar to the zap , the Ruby logger is ongoing, with several contributions currently under review.
3. **SwiftLog Integration**: For the Swift programming language, I contributed to integrating OTel with SwiftLog. This integration ensures that log messages can be correlated with trace data, enhancing observability in iOS and macOS applications. The SwiftLog integration is also a work in progress, with ongoing reviews and refinements. 
   
   Grateful to the feedbacks provided by @IgnacioBonafonte 


Engaging with the Community:
My journey with OpenTelemetry has been transformative. I have enjoyed every part of it - from interacting with Special Interest Groups (SIGs) to sitting quietly in a room thinking of a solutions. This was the engineering I wished to do.

For those looking to contribute to open-source projects, I highly recommend seeking out mentorship programs like LFX. And I also hope the community will find these contributions helpful.





For new contributions:
- Improve documentation around project architecture, design patterns and caveats.
- Add good first issues/help wanted tags
- Make a lot of noise about how the community is excited to have new contributors?
- quicker feedback process

How can we improve diversity
- Diverse recruitment is what I can think for now