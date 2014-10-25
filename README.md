# resilient-server

Dummy HTTP server fully compatible with the [Resilient](http://resilient-http.github.io) [specfication](https://github.com/resilient-http/spec) discovery protocol for demo/development/testing proposals

## Installation

You must have [node.js](http://nodejs.org) already installed

Install the package
```bash
npm install -g resilient-server
```

Start the server
```bash
resilient-server -p 8080 -h 0.0.0.0 --api-key awesome
```

## API

#### GET /:appName

Get a list of servers for the given application service

##### Request

```
curl -i http://localhost:8080/my-app-api
```

##### Response

Valid response
```json
HTTP/1.1 200 OK

[
  "http://api1.server.me",
  "http://api2.server.me",
  "http://api3.server.me"
]
```

Missing app name
```
HTTP/1.1 404 Not Found
```

#### POST|PUT /:appName

Update the servers for the given application service

**Note**: this service could require an API key token, if it's was defined

##### Request

```
curl -i -H "Accept: application/json" \
  -H "API-Token: awesome" \
  -X POST -d '["http://newapi.server.com"]' \
  http://localhost:8080/my-app-api
```

##### Response

Valid response
```
HTTP/1.1 204 No Content
```

Invalid response
```
HTTP/1.1 400 Bad Request
```

#### DELETE /:appName

Removes the servers of a given app from the registry

##### Request

```
curl -i -H "Accept: application/json" \
  -H "API-Token: awesome" \
  -X DELETE  \
  http://localhost:8080/my-app-api
```

##### Response

Valid response
```
HTTP/1.1 204 No Content
```

Invalid response
```
HTTP/1.1 404 Not Found
```

## Development

You must have installed [node.js](http://nodejs.org) >= `0.10`

Clone this repository

```bash
git clone https://github.com/h2non/resilient-server.git && cd resilient-server
```

Install runtime and developmennt dependencies

```bash
npm install
```

Run tests

```bash
grunt test
```

Run the server

```
./bin/resilient-server --port 8080 --debug
```

Show help

```
./bin/resilient-server --help
```

Run as a service (using [forever](https://github.com/nodejitsu/forever))

```bash
forever -m 5 ./bin/resilient-server
```

## License

MIT - Tomas Aparicio