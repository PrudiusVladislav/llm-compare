# Project wide logging
This is a prompt for solving the Task 3 - case of a project without proper observability stack, using just console.log. 
The task requires LLM to set up certain observability tools and migrate the project to use them instead of default console.
The prompt:

```
You need to add proper logging to this codebase. Right now we just have random console.logs scattered everywhere and it's a mess to debug in production.

Here's what I'm thinking:

Backend logging - we should use pino for structured logging. It should work in dev with pretty-printing and in prod we need to ship logs to Grafana Loki. We will have the loki credentials in env vars.

Frontend observability - for client-side we want to use Grafana Faro. It should capture console logs and errors and send them to our Faro collector. Skip this in dev mode.

Request context - Each request should have a logger in event.locals that carries context like the user's id, a session id, and a ray/trace id from cloudflare or aws headers.

Svelte components - We need a way for components to get a logger. Maybe use Svelte's context API - we could set the logger meta in a context in layout and then have a helper function to create child loggers from it.

Replace the console.logs in the codebase with proper logger calls where it makes sense. The log level should be configurable via PUBLIC_LOG_LEVEL (default to 'info').

The main files to create should probably go under src/lib/observability/.
```
