# url

*   Properties

    ```
    ┌─────────────────────────────────────────────────────────────────────────────┐
    │                                    href                                     │
    ├──────────┬┬───────────┬─────────────────┬───────────────────────────┬───────┤
    │ protocol ││   auth    │      host       │           path            │ hash  │
    │          ││           ├──────────┬──────┼──────────┬────────────────┤       │
    │          ││           │ hostname │ port │ pathname │     search     │       │
    │          ││           │          │      │          ├─┬──────────────┤       │
    │          ││           │          │      │          │ │    query     │       │
    "  http:   // user:pass @ host.com : 8080   /p/a/t/h  ?  query=string   #hash "
    │          ││           │          │      │          │ │              │       │
    └──────────┴┴───────────┴──────────┴──────┴──────────┴─┴──────────────┴───────┘
    ```

    ```
    urlObject.href
    urlObject.protocol
    urlObject.slashes
    urlObject.auth
    urlObject.host
    urlObject.hostname
    urlObject.port
    urlObject.path
    urlObject.pathname
    urlObject.search
    urlObject.query
    urlObject.hash
    ```

*   Methods

    ```
    url.format(urlObject)
    url.parse(urlString[, parseQueryString[, slashesDenoteHost]])

    url.resolve(from, to)
    ```

