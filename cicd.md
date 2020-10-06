## CI/CD

### Traditional integration problems 
* Multiple developers working in isolation and delaying integration until a later point
* Release builds performed on developer hardware (no assurance code on developer machine matches source repository tests)
* Tests might exist but must be executed manually
* Release performed manually

### Solution: CICD 
Check-in code --> Source repository --> CI server [build, test, result] --> Test --> Staging --> Production (auto)

### Continuous Integration 
* Development practice where members of a team integration their work frequently (at least daily)
* Integrations are verified by an automated build (including tests), this leads to reduced integration problems and faster development of a cohesive software

### CI core practice
* Maintain a single source repository 
* Automate the build 
* Make your build self-testing
* Everyone commits to the baseline every day
* Every commit should build on an itegration machine 
* Keep the build fast (don't take more than 10 min)

### Continuous delivery and why 
* a development discipline where sotware is built in such a way that it can be released to production at any time

### CICD/Build server (Jenkins automation)
* Provides a central service to:
    * Build 
    * Test 
    * Scan 
    * Deploy applications
    * Continuous integration and delivery (CI/CD)
* Integrated with the cloud infrasturcture, control platforms, chat agents, authentication solutions and repositories
* Bitbucket, Jenkins an cloud technologies ensure builds are automated, scalable and elastic 

### Static vs. Dynamic Scanning 
* Why? to identify application weaknesses and identify application vulnerabilities. To either prevent or remediate weakness of an applicatin. 
* Static: when application is not in run time
* Dynamic: when applicatin is running 

### Static scan
* S3: static scanning: scans all static code for all applications in the firm. 
* Fortify AWB
* Open source scanning: scans the open source components/libraries used by an application
   * Apche boi 
   * Blackduck: for lagency/retiring projects 
   * Raven 
   * OSS scan management 
     * Soteria

### Flow of source code 
Initialize (bitbucket webhook with cicd server) --> build --> test --> scan --> publish --> deploy
