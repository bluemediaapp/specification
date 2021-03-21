# Stack

## Monitoring

Prometheus should be included in all services with a public readonly grafana server to be as open as possible to the
community

## Services

### Caching

Caching should be done through redis or by storing it in a temporary container file system  
Caching on the file system should ONLY be used for big files

### Indexing

Indexing should be done through redis and postgres.  
Redis for short term & often requested data and postgres for large amounts of small data not so often requested

### Compression/resizing

Compression should be done through a golang compression and resizing server

### CDN

Should be written in golang using fiber, which should be verifying hashes, unzipping, indexing and caching

### Recommendation service
This should be able to be written in any language/framework as performance shouldn't be a huge issue

### Backend
This should be a catch-all backend which will handle most things like reports, notifications etc  
Should be able to be written in any language

### Web-Frontend
Frontend for the desktop, preferably written in react and served via go-fiber.  
A PWA would be nice but not needed.

### Mobile-Frontend
Frontend written in react native or java.
