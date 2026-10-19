# Groovy patterns for SAP Cloud Integration

Verify runtime-specific behavior (Groovy version, available libraries) against current SAP documentation before relying on it.

## Contents
- Script skeleton
- Headers, properties, body
- Message processing log
- XML and JSON handling
- Exception handling
- Common pitfalls

## Script skeleton

```groovy
import com.sap.gateway.ip.core.customdev.util.Message

def Message processData(Message message) {
    // logic here
    return message
}
```

The script step expects a `processData(Message message)` function that returns the message.

## Headers, properties, body

```groovy
def h = message.getHeader('MyHeader', String)          // null if absent
message.setHeader('MyHeader', 'value')

def p = message.getProperty('MyProperty')               // null if absent
message.setProperty('MyProperty', 'value')

String body = message.getBody(String)
message.setBody(newBody)
```

Guard against null and blank values (`h?.trim()`), not just missing ones. Header-name case handling can differ by source and adapter, so verify with a trace.

## Message processing log

```groovy
def log = messageLogFactory?.getMessageLog(message)
log?.setStringProperty('OrderId', orderId)
log?.addAttachmentAsString('Debug', 'non-sensitive text', 'text/plain')
```

`messageLogFactory` is provided to CPI scripts. Only attach non-sensitive data, and keep attachments small.

## XML and JSON

```groovy
import groovy.json.JsonSlurper
import groovy.json.JsonOutput
import groovy.xml.XmlUtil

def json = new JsonSlurper().parseText(message.getBody(String))
def out = JsonOutput.toJson(map)

def xml = new XmlSlurper().parseText(message.getBody(String))
String text = XmlUtil.serialize(xml)
```

- Check namespaces explicitly when a lookup returns empty unexpectedly.
- Treat missing nodes as empty, not as errors, unless the contract says otherwise.
- For large payloads consider streaming (`message.getBody(java.io.InputStream)`) instead of loading a large String.

## Exception handling

Inside an exception subprocess the caught exception is commonly read from the `CamelExceptionCaught` property:

```groovy
def ex = message.getProperty('CamelExceptionCaught')
String cls = ex?.getClass()?.getCanonicalName()
String msg = ex?.getMessage()
```

Some exception types expose extra details (for example HTTP status or response body). Confirm the exact type and its methods in a trace before depending on them.

## Common pitfalls

- Using `SimpleDateFormat` as a shared or static object (not thread-safe). Prefer `java.time`, and always set an explicit time zone.
- Assuming UTF-8. Check the source encoding and the charset headers.
- Logging whole payloads or tokens.
- Swallowing exceptions so the failure disappears from monitoring. Rethrow with context.
- Relying on default namespace behavior without testing real payloads.
- Building large strings with repeated concatenation inside loops.
