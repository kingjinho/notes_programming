# Proxy Pattern

- Be careful to use
    - Since it mitigates the meaning of a class

## Proxy?

- Proxy Server
    - `Server that sits between website and users`
    - `Works like cache memory`
    - If proxy server has a document, return it
        - otherwise, get from real server and save it in proxy server

- Sometimes, it's hard to keep states in a class
    - data too large
    - take too long to load data
    - not frequently used

## Example: Image data

- Good for applying proxy pattern
- Image data tends to be large
- Load when it's needed
    - Lazy Loading
    - The opposite is `eager loading`