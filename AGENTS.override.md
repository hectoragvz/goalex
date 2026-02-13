This is a template API built entirely with GO from Alex Edward´s Let´s Go Further book, intended to be easily spin up to other backend projects with a tweak on the endpoints, data objects (since not all apps deal with movies lol), and auth.

We write an AGENTS.md file per directory for use with LLMs.

## Information

It’s important to be aware that httprouter doesn’t allow conflicting routes which potentially
match the same request. So, for example, you cannot register a route like GET /foo/new and
another route with a parameter segment that conflicts with it — like GET /foo/:id .
