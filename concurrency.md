
## Concurrency computing and thread safety

### Concurrecy 
`Concurreny computing`
on several core: computation executed in parallel

`Concurrency control`
on one core: seems parallel, like round robin, have a shared resources

`Thread`
the smallest sequence of programmed instructions that can be managed independently by a scheduler 

`Immutable object`
an object whose state cannot be changed after creation (finally)

`Mutable object`
An object whose state can be modified after creation 

`Compound actions`
An action made up of individual discrete steps that re generally executed together, atomically 

`Atomic`
action or objec that is essentially indivisible, unchangeable, whole or irreducable 

### Concurrency cheat sheet
Mutable state: the less the better
Immutable objects are automatically thread safe
Guard all mutables with a lock 
Hold all locks for the duration of compund (or atomic) actions 

### Thread safe
1. Add `synchronized` to a method makes it thread safe because the class object will be locked when it's executed.
https://www.programcreek.com/2014/02/how-to-make-a-method-thread-safe-in-java/
https://www.baeldung.com/java-thread-safety

### P.S.
Don't create a thread for each evet received, use a thread pool for incoming requrests and reuse them 
System.out.println is not thread safe
Put a thread indicator and timestampe in og statements 
