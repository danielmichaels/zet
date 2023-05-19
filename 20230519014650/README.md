# API project design

A rough outline of how I'll implement an API for a project I'm developing
using `oapi-codegen`.

Endpoints:

```yaml
/healthz:
    - GET
/users:
    - GET
    - POST
    - PATCH
    - DELETE
/monitors:
    - GET
/monitors/{monitor-type}:
    - GET
    - POST
    - PATCH
    - DELETE
/monitors/{monitor-type}/{monitor:id}
    - GET
    - POST
    - PATCH
    - DELETE
```

The barebones are there but implementation needs some work.

Tags:

    #planing #openapi #go
