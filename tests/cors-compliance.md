# Test: CORS Compliance

This test will check the availbility of CORS specific headers

1. Support CORS (Cross Origin Resource Sharing) from `access-control-allow-origin` (default = `*`)
   origins
    1. Request with Origin: (default: vliz.be or Github project name)
    2. Also check for redirects
2. Support CORS for the `access-control-allow-methods` (default = `GET`, `HEAD`, `OPTIONS`) methods.
    1. Also check for redirects
3. `access-control-allow-headers` (default = `Accept`): in response to a HTTP OPTIONS (preflight)
   request to indicate which headers can be used during the actual request.
4. `access-control-expose-headers` (default = `Content-Type, Link`): indicates which response
   headers should be made available to scripts running in the browser in response to a cross-origin
   request (these are additional headers to
   the [CORS-safelisted](https://developer.mozilla.org/en-US/docs/Glossary/CORS-safelisted_response_header)
   response header).
5. Http redirects to https (because it's impossible to access http from https)

### MoSCow:

| Number | Name                          | MoSCoW |
|--------|-------------------------------|--------|
| 1      | access-control-allow-origin   | Must   |
| 2      | access-control-allow-methods  | Must   |
| 3      | access-control-allow-headers  | Must   |
| 4      | access-control-expose-headers | Should |
| 5      | redirect to https             | Should |

Example configuration:

```yaml
test:
  cors-compliance:
    image: ghcr.io/grmp-tests/cors-compliance:latest
    config:
      access-control-allow-origin: '*'
      access-control-allow-methods: 'GET, HEAD, OPTIONS'
      access-control-allow-headers: 'Accept, X-Custom-Header'
      https-redirect: true
```