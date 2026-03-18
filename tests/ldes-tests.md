# Test: LDES Tests

This test will check the compliance of a [Linked Data Event Stream (LDES)](https://semiceu.github.io/LinkedDataEventStreams/) endpoint.

1. The endpoint returns a valid LDES stream
   1. Response contains a resource typed as `ldes:EventStream`
   2. Response uses a supported RDF content type (e.g., `text/turtle`, `application/ld+json`)
2. LDES metadata is present
   1. `ldes:timestampPath` is defined
   2. `ldes:versionOfPath` is defined (optional, for versioned streams)
3. Tree (pagination) compliance
   1. Root node is typed as `tree:Node`
   2. `tree:member` predicates are present (or linked via `tree:view`)
   3. `tree:Relation` objects are valid when present
      1. Each relation has a `tree:node` pointing to the next page
      2. Each relation has a valid `tree:relationType` (e.g., `tree:GreaterThanOrEqualToRelation`)
      3. Navigation through all relations/pages is possible without errors
4. Member validation
   1. Members are valid RDF
   2. Members conform to the expected type (`shape` or `memberType` if configured)

### MoSCow:

| Number | Name                                      | MoSCoW |
|--------|-------------------------------------------|--------|
| 1      | Valid LDES stream                         | Must   |
| 2.1    | ldes:timestampPath present                | Should |
| 2.2    | ldes:versionOfPath present                | Could  |
| 3.1    | Root node typed as tree:Node              | Must   |
| 3.2    | tree:member or tree:view present          | Must   |
| 3.3    | tree:Relation navigation                  | Should |
| 4.1    | Members are valid RDF                     | Must   |
| 4.2    | Members conform to expected type/shape    | Could  |

Example configuration:
```yaml
test:
  ldes-tests:
    image: ghcr.io/grmp-tests/ldes-tests:latest
    config:
      url: https://brugge-ldes.geomobility.eu/observations
      member-type: https://schema.org/Observation
      check-member-conformity: false
```
