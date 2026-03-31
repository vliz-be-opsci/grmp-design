# Test: LDES Tests

This test will check the compliance of a [Linked Data Event Stream (LDES)](https://semiceu.github.io/LinkedDataEventStreams/) endpoint.

1. The endpoint returns a valid LDES stream
   1. Response contains a resource typed as `ldes:EventStream`
   2. Response uses a supported RDF content type (e.g., `text/turtle`, `application/ld+json`)
2. LDES metadata is present
   1. `ldes:timestampPath` is defined
   2. `ldes:versionOfPath` is defined
   3. Member type is inferred from the LDES feed itself
3. Tree (pagination) compliance
   1. Root node is typed as `tree:Node`
   2. `tree:member` predicates are present (or linked via `tree:view`)
   3. `tree:Relation` objects are valid when present
      1. Each relation has a `tree:node` pointing to the next page
      2. Each relation has a valid `tree:relationType` (e.g., `tree:GreaterThanOrEqualToRelation`)
      3. Navigation through all relations/pages is possible without errors
4. Member validation
   1. Members are valid RDF
   2. Members conform to the expected type (inferred from the LDES feed)
   3. If `shape_validation_file` is configured, each member is validated against the given SHACL shape file

### MoSCow:

| Number | Name                                      | MoSCoW |
|--------|-------------------------------------------|--------|
| 1      | Valid LDES stream                         | Must   |
| 2.1    | ldes:timestampPath present                | Must   |
| 2.2    | ldes:versionOfPath present                | Must   |
| 3.1    | Root node typed as tree:Node              | Must   |
| 3.2    | tree:member or tree:view present          | Must   |
| 3.3    | tree:Relation navigation                  | Must   |
| 4.1    | Members are valid RDF                     | Must   |
| 4.2    | Members conform to expected type/shape    | Could  |

Example configuration:
```yaml
test:
  ldes-tests:
    image: ghcr.io/grmp-tests/ldes-tests:latest
    config:
      url: https://brugge-ldes.geomobility.eu/observations
      min_fragment: 1
      min_members: 10
      shape_validation_file: https://example.org/shapes/observation.ttl
      min_last_modified_date: 2024-01-01T00:00:00Z
```
