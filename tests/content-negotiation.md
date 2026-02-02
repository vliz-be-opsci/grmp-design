# Test: Content Negotiation

This test will check the content negotiation and its response

1. Supports basic content negotiation
   1. `text/turtle`
   2. `application/ld+json`
   3. `application/trig`
   4. ...
2. Supports extended content negotiation
   1. `Accept: application/ld+json, application/trig;q=0.98, text/turtle;q=0.95, application/n-quads;q=0.9, application/n-triples;q=0.9, application/rdf+xml;q=0.5, text/html;q=0.3, */*;q=0.1`
3. For all content types: check if response body conforms the content type

### MoSCow:

| Number | Name                               | MoSCoW |
|--------|------------------------------------|--------|
| 1      | Basic content negotiation          | Must   |
| 2      | Extended content negotiation       | Should |
| 3      | Check response body                | Should |


Example configuration:
```yaml
tests:
  content-negotiation:
    image: ghcr.io/grmp-tests/content-negotiation:latest
    config:
      url: https://brugge-ldes.geomobility.eu/observations
      supports-content-types:
        - text/turtle
        - application/trig
      check-response-body-conformity: true
```