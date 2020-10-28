Using Webpack Dev Server, Server-Sent-Events aren't picked up by the Javascript
EventSource. The EventSource `onopen` fires, but not any listeners.

Two options to fix this:

1. Disable compression in the webpack devserver config.
2. Send `Content-Type: no-transform` in the response header.
