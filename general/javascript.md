# Javascript

## Fetch

### Example: GET

```javascript
fetch('/api/something')
.then(res => 
    return res.json();
})
.then(json => {
    doSomething(json);
})
.catch(err => {
    console.warn(err);
});

```

### Example: POST

```javascript
const data = {name: 'bob'}:
const headers = new Headers({'Content-Type': 'application/json'});

fetch('/api/something', {
    method: 'POST',
    body: JSON.stringify(data),
    headers: headers
})
.then(res => 
    return res.json();
})
.then(json => {
    doSomething(json);
})
.catch(err => {
    console.warn(err);
});

```
