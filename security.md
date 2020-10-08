
## Security 

### Best practice part 1
* Restrict inputs and perform input (JSON/XML) sanitization and validation

Input sanitization describes cleansing and scrubbing user input to prevent it from jumping the fence and exploiting security holes. But thorough input sanitization is hard. While some vulnerable sites simply don’t sanitize at all, others do so incompletely, lending their owners a false sense of security.
* SQL injection 
* Cross-site scripting 
* Remote file inclusion 

* [Encode/Escape outputs that are returned to the client](https://cwe.mitre.org/data/definitions/116.html)

Improper encoding or escaping can allow attackers to change the commands that are sent to another component, inserting malicious commands instead.

Most software follows a certain protocol that uses structured messages for communication between components, such as queries or commands. These structured messages can contain raw data interspersed with metadata or control information. For example, "GET /index.html HTTP/1.1" is a structured message containing a command ("GET") with a single argument ("/index.html") and metadata about which protocol version is being used ("HTTP/1.1").

If an application uses attacker-supplied inputs to construct a structured message without properly encoding or escaping, then the attacker could insert special characters that will cause the data to be interpreted as control information or metadata. Consequently, the component that receives the output will perform the wrong operations, or otherwise interpret the data incorrectly.

* Implement session management/timeout when in control of application 

Session management is the practice of managing the user's interactions with a web application. Since HTTP calls are stateless, session management is used to ensure proper access controls and authorization for each HTTP transaction. 

There are 2 types: `cookie` and `URL rewriting`.  

* Use encryption protocols and algorithm 

`SSL`: secure sockets layer - security certificate protocol that uses encryption for when packets of data is sent when 2 systems on the internet. It keeps data safe, or unreadable, as it is being transferred over the network.

`TSL`: transport layer security - upgraded version of SSL

Asymmetrical cryptography: safest method - uses 2 keys (public and private key). Symmetrical cryptography 

TSL starts a session using asymmetrical cryptography in conjunction with hashing via a handshake.

HTTPS: secure HTTP request that means a website us secured by a SSL certificate

* Provide minimal error messages to end user as to not divulge possible code weak points
  * Don't log user input when possible as a database is more secure than a plain text log file
  * Log only pertinent information using the proper log level - info, error, fatal, warn, debug, and trace
  * Ensure the logs contains specifics to help identify any bugs or issues
  * Errors are bugs in the code that require programmtic intervention to fix; 
  * An exception is a use case where an error was expected and caught by the code and is handled gracefully 

* Scan code prior to release and resolve any known vulnerabilities

* Implement secure authentication and authorization mechanisms
  * Use multi-factor authentication for login methods
  * Use password hashing 
  * Use HTTPS post methods only when transmitting passwords
  * Use least priviledge model for authorization mechanisms
  * Moneta boot security 

* Maintain security audit logging 
It is a best practice to log the following events:
  * Successful/Unsuccessful authentication attempts
  * OS system events: network failure, service restarts, etc
  * Audit events - user account changes, file system changes
  * Error/Exception events
  * App events - startup/shutdown, failures, etc
  * All logs should include: timestamp, user who completed the action, what action was performed/happpened, system that was accessed, any system or error code/details, and device used(IP address, etc)

* Have code reviews 
Review a small chunks of code at a time (less than 400 LOC) as quality of the review is important for bug/defect identification

### Best practice part 2

