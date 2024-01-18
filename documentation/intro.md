## Basic explanation



## Content
It contains several configurations base for appender:
For log4j2
- Tjahzi  which provides a log4j2 appender as well as logback appender.
  https://github.com/tkowalcz/tjahzi

For logback
- There is also Loki4j project which seems to provide a fine logback appender.
  https://github.com/loki4j/loki-logback-appender

## Other options

You can use promtail to replicate the log, but as a file system detection it opens a container that loads too much the server
The trace of the file increases the network traffic as it needs to detect the fs changes and send it over

Problem:
- The system needs to read an external fs with a time window (15s for instance). If the pod fails during that time, there won´t be traces

This approach seems cleaner and more versatile as the logging system pushes the content as fast as it generates.

### References

Promtail
https://jarirajari.wordpress.com/tag/promtail/
https://grafana.com/docs/loki/latest/send-data/promtail/troubleshooting/


TEA talk (very good!)
https://github.com/jonatan-ivanov/teahouse
https://www.youtube.com/watch?v=CaoVtKK7sxM&list=PLXADOFXCGUmXAWeVWIQ40HNrezC4ulgRW

Micrometer vs opentelemetry
https://docs.micrometer.io/tracing/reference/
https://grafana.com/docs/opentelemetry/instrumentation/java/spring-starter/
https://grafana.com/grafana/dashboards/18812-jvm-overview-opentelemetry/

Similar projects
https://github.com/marcingrzejszczak/observability-boot-blog-post/blob/main/server/pom.xml
https://github.com/sivaprasadreddy/devzone

Loki appender
https://loki4j.github.io/loki-logback-appender/docs/configuration
https://github.com/grafana/loki/blob/main/production/docker/config/loki.yaml

Other fonts
https://www.youtube.com/watch?v=0B-yQdSXFJE