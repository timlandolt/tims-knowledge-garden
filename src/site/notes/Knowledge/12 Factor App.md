---
{"dg-publish":true,"permalink":"/knowledge/12-factor-app/"}
---

---

## What is a 12 Factor App?
The 12 Factor App is a methodology to develop SaaS apps.

A 12 Factor App
- Uses **declarative** formats for setup automation, to minimize time and cost for new developers joining the project;
- Have a **clean contract** with the underlying operating system, offering **maximum portability** between execution environments;
- Are suitable for **deployment** on modern **cloud platforms**, obviating the need for servers and systems administration;
- **Minimize divergence** between development and production, enabling **continuous deployment** for maximum agility;
- And can **scale up** without significant changes to tooling, architecture, or development practices.

## The 12 Factors of a 12 Factor App
### 1. Codebase
*One codebase tracked in revision control, many deploys*

- Tracked with version control.
- Codebase and App are the same. If there are multiple codebases it is a distributed system (each component may be a 12 Factor App)
- If multiple apps share some code, the shared code should be extracted into a library.
- The codebase is the same across the deploys (including local development environments) but the version of the codebase might vary.

### 2. Dependencies
*Explicitly declare and isolate dependencies*

- A twelve-factor app never relies on implicit existence of system-wide packages.
	=> All dependencies are declared explicitly in a manifest
- It uses a dependency isolation tool during execution

=> In [[Knowledge/Ruby on Rails\|Rails]]: `Gemfile` as manifest and `bundle exec` for dependency isolation

### 3. Config
*Store config in the environment*

Here, config are defined to contain everything that might vary between deploys.
So i.e. Routes do not count.

- Configs should be strictly separated from code.
	- To see if this is the case you can think about, if it would be possible to make the project open source (without the config)
- Actually, configs should be stored in environment variables. This for one makes it secure, but also it allows for granular control in each environment.

### 4. Backing Services
*Treat backing services as attached resources*

A backing service is any service the app consumes over the network as part of its normal operation. (Datastores, messaging/querying systems, SMTP services and caching systems)

- The code should make no distinctions between local and third party services
- The resources have to be exchangeable by just changing the values in the config.

### 5. Build, release, run
*Strictly separate build and run stages*

**Build stage**: converts the code repo into an executable bundle = the build
**Release stage**: the build is combined with the environments' config. The resulting release is ready for immediate execution.
**Run stage**: aka runtime runs the app in the execution environment.

- These stages are strictly separated. For example, that the code cannot be changed at runtime. 
- Each release should have a unique ID like a timestamp or an incrementing number

### 6. Processes
*Execute the app as one or more stateless processes*

- The individual processes should be stateless and share nothing. Data that needs to persist must be stored in a backing service like a database.
- A 12-Factor App doesn't assume that a file in memory or on disk will be available for long. This means files can be downloaded briefly to operate on, but the result should then be stored in a database.

### 7. Port binding
*Export services via port binding*

- A 12-Factor app doesn't depend on an external web server (like Apache for PHP). The app directly binds to a port. This is achieved by using a web server library.

### 8. Concurrency
*Scale out via the process model*

- Break the app into functional roles.
- Scale horizontally, not vertically
- Because processes are stateless (Factor 6), they can run on different physical machines without needing to talk to each other.
- The app should not try to manage itself (no daemonizing). It relies on an external process manager (like systemd or Kubernetes) to start/stop processes and handle crashes.

### 9. Disposability
*Maximize robustness with fast startup and graceful shutdown*

- Processes shut down gracefully when they receive a SIGTERM signal from the process manager.
- HTTP: No new requests get handled, the current ones get completed before shutting down.
- Workers: If a job is locked, it should be unlocked. After that the job is returned to the queue.

### 10. Dev/prod parity
*Keep development, staging, and production as similar as possible*

|                                | Traditional app  | Twelve-factor app      |
| ------------------------------ | ---------------- | ---------------------- |
| Time between deploys           | Weeks            | Hours                  |
| Code authors vs code deployers | Different people | Same people            |
| Dev vs production environments | Divergent        | As similar as possible |
This also means that the same backing services (like DBs) should be used in all the environments (no SQLite for local development)

### 11. Logs
*Treat logs as event streams*

- Logs should be written to `stdout` this is all the app should concern.
- In staging and production deploys the stream is then handled by the execution environment. There it is collated with the other log streams and routed to a final destination where it then is archived.

### 12. Admin Processes
*Run admin/management tasks as one-off processes*

- Admin tools must be part of the same code deployment (repo) as the app itself to prevent version mismatches.
- Every one-off script must use the exact same config and environment as the live app.
- Run admin tasks in their own process so they don’t hog memory or crash the web server, but let them talk to the same database.
- Use the REPL: Favor languages that let you "remote into" the app’s brain (like `rails console` or `django shell`) to inspect live data safely.
