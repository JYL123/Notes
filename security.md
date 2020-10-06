
## Security 

### Restrict inputs and perform input (JSON/XML) sanitization and validation

Input sanitization describes cleansing and scrubbing user input to prevent it from jumping the fence and exploiting security holes. But thorough input sanitization is hard. While some vulnerable sites simply don’t sanitize at all, others do so incompletely, lending their owners a false sense of security.
* SQL injection 
* Cross-site scripting 
* Remote file inclusion 

### [Encode/Escape outputs that are returned to the client](https://cwe.mitre.org/data/definitions/116.html)

Improper encoding or escaping can allow attackers to change the commands that are sent to another component, inserting malicious commands instead.

Most software follows a certain protocol that uses structured messages for communication between components, such as queries or commands. These structured messages can contain raw data interspersed with metadata or control information. For example, "GET /index.html HTTP/1.1" is a structured message containing a command ("GET") with a single argument ("/index.html") and metadata about which protocol version is being used ("HTTP/1.1").

If an application uses attacker-supplied inputs to construct a structured message without properly encoding or escaping, then the attacker could insert special characters that will cause the data to be interpreted as control information or metadata. Consequently, the component that receives the output will perform the wrong operations, or otherwise interpret the data incorrectly.

### Implement session management/timeout when in control of application 

### Use encryption protocols and algorithm 

### Provide minimal error messages to end user as to not divulge possible code weak points

### Scan code prior to release and resolve any known vulnerabilities

### Implement secure authentication and authorization mechanisms

### Maintain security audit logging 

### Have code reviews 

