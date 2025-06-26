### API Server
```http
  https://key-verification-01a8d1.netlify.app/.netlify/functions/
```

### API Documentation
- [Request key](#request-key-(token))
- [Generate key](#generate-key)
- [Validate key](#validate-key)
- [Optional settings](#optional-settings)

### Request key (token)
```http
  POST /create-keygen-request
```

### Example
```javascript
const res = await fetch('https://key-verification-01a8d1.netlify.app/.netlify/functions/create-keygen-request', {
  method: 'POST',
  headers: { 'Content-Type': 'application/json' },
  body: JSON.stringify({
    origin: window.location.origin
  })
});
const { token } = await res.json();
if (data.token) {
  window.open('https://key-verification-01a8d1.netlify.app/?origin=' + data.token, '_blank');
} else {
  alert(data.error || 'Error when requesting the token!');
}
```

### Generate key
```http
  POST /generate-key
```
```javascript
const res2 = await fetch('https://key-verification-01a8d1.netlify.app/.netlify/functions/generate-key', {
  method: 'POST',
  headers: { 'Content-Type': 'application/json' },
  body: JSON.stringify({ origin: token })
});
const { key } = await res2.json();
```

### Validate key
```http
  POST /validate-key
```
```javascript
const res3 = await fetch('https://key-verification-01a8d1.netlify.app/.netlify/functions/validate-key', {
  method: 'POST',
  headers: { 'Content-Type': 'application/json' },
  body: JSON.stringify({
    key,
    origin: window.location.origin
  })
});
const { valid } = await res3.json();
```

### Optional settings

| Field | Type     | Standard                | Description                | Restriction                |
| :-------- | :------- | :------------------------- | :------------------------- | :------------------------- |
| `origin	` | `string` | -- | Your website, e.g. window.location.origin | **Required** |
| `length	` | `number` | 8 | Length of the key | min: 4, max: 24 |
| `prefix	` | `string` | "" | 	Prefix for the key | optional |

### Example with settings
```javascript
const res = await fetch('https://key-verification-01a8d1.netlify.app/.netlify/functions/create-keygen-request', {
  method: 'POST',
  headers: { 'Content-Type': 'application/json' },
  body: JSON.stringify({
    origin: window.location.origin,
    length: 12,      // optional, min: 4, max: 24
    prefix: 'abc-'   // optional
  })
});
```
