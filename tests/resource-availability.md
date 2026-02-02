# Test: Resource Availability

This test will check the availability of a resource or LDES stream.

1. DNS resolves to IP Address
2. Check if response status is 200 code 
   1. If response status is 3xx, follow new location and check for 200 code 
   2. Accept only `max-redirects` (default = 0) number of redirects
3. Track response time 
   1. If > `timeout` seconds (default = 30 s) -> ERROR 
4. Availability via http and/or https 
   1. If `check-http-availability=true` (default = `false`) and not available -> ERROR
   2. If `check-https-availability=true` (default = `true`) and not available -> ERROR

### MoSCow:

| Number | Name                                 | MoSCoW |
|--------|--------------------------------------|--------|
| 1      | DNS resolves                         | Must   |
| 2      | Check if response status is 200 code | Must   |
| 3      | Track response time                  | Must   |
| 4      | Availability via http and/or https   | Should |


Example configuration:
```yaml
test:
  resource-availability:
    image: ghcr.io/grmp-tests/resource-availability:latest
    config:
      url: https://brugge-ldes.geomobility.eu/observations
      max-redirects: 3
      timeout: 10
      check-http-availability: false
      check-https-availability: true
```