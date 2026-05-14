# Request Query Accessors

The Quantum PHP Framework provides methods for interacting with request query parameters directly from the `Request` object.

## Query Accessors

The `Query` trait provides the mechanism for reading and modifying the raw query string associated with the current request.

### `getQueryParam(string $key): ?string`

This method returns the **first-match raw value** for the specified key from the current request's query string.

- **Note on decoding**: It returns the raw value exactly as it appears in the query string; it **does not URL decode** the value.
- **Return value**: Returns the raw value if found, or `null` if the key is not present in the query string or if the query string is unset.

**Examples:**

```php
// Assuming current query string: "id=123&name=John%20Doe"

$request->getQueryParam('id');   // Returns "123"
$request->getQueryParam('name'); // Returns "John%20Doe"
$request->getQueryParam('age');  // Returns null
```

### `setQueryParam(string $key, string $value): void`

This method appends a new query parameter to the query string.

- **Non-overwriting**: It does not overwrite existing keys. If a key already exists, appending will result in duplicate keys in the raw query string.
- **Encoding contract**: The framework **does not URL-encode** the key or value. Callers are responsible for encoding values if they contain spaces or special characters.

**Example:**

```php
// Initial state: query string is null

$request->setQueryParam('user', 'arman');
// Query string: "user=arman"

// Appending with special characters (no automatic encoding)
$request->setQueryParam('message', 'hello world'); 
// Raw query string: "user=arman&message=hello world"

// Appending an existing key (duplicate keys)
$request->setQueryParam('id', '1');
$request->setQueryParam('id', '2');
// Raw query string: "user=arman&message=hello world&id=1&id=2"
```
