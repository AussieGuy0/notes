# vue

## Proxy for development
Change proxytable in config/index.js to something like:

```
// any request to /api will be rerouted
proxyTable: {
        '/api': {
            target: 'http://localhost:4567',
            changeOrigin: true
        }
}
```
