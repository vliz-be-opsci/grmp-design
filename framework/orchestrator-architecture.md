# Orchestrator architecture

1. Orchestrator in Python, uses [Docker SDK for Python](https://docker-py.readthedocs.io/en/stable/)
2. Reads the configuration file (YAML) and controls workers (= tests)
3. Each test that is run in a container that receives input parameters via the orchestrator (from
   the configuration file) and is expected to produce a Junit XML -->
   See [Report format](./report-format.md)
4. Orchestrator retrieves these Junit XMLs (via volumes, already tested in a simple ‘Hello World’
   example) and merges them into a final report. Junitparser is probably the most suitable library;
   ‘junit-xml’ is slightly less suitable for merging.
5. Orchestrator is in a separate repository (public or private with credentials, agreement with
   customer), github actions triggered from either same or another repo with configuration file.
6. Final report is committed in repository which triggered the github actions and which contains the
   configuration file. Github actions in this repository configure github pages to visualize the
   data in this final report.
7. Local: simple docker-compose with orchestrator as the only main resource, containers that perform
   the tests are fully managed by the orchestrator.
8. Manageability of configuration:
   1. Split config in multiple (sub-)directories and files
   2. Possible to define parent-like configuration (eg list of urls) that can be overridden in
   specific configuration for the test
9. Amelioration of configuration:
   1. Enable resolving of data (eg from environment variables) in the configuration
   2. Add more semantic to input parameters and output properties
10. Amelioration of test report:
   1. Ability to add heuristics / possible pattern to solve the problem to report
   2. Add logs and/or stack trace when a test fails

### MoSCow:

| Number | Name                                  | MoSCoW | Priority (in respect to MoSCoW) |
|--------|---------------------------------------|--------|---------------------------------|
| 1      | Orchestrator in Python                | Must   | 1                               |
| 2      | Reads the configuration file          | Must   | 1                               |
| 3      | Test in container, input and output   | Must   | 1                               |
| 4      | Merge final report                    | Must   | 1                               |
| 5      | Trigger from separate repo            | Must   | 2                               |
| 6      | Commit final repo                     | Must   | 2                               |
| 7      | Run locally                           | Must   | 1                               |
| 8.1    | Multiple config files                 | Could  | 1                               |
| 8.2    | Parent configuration                  | Could  | 2                               |
| 9.1    | Resolving of data                     | Could  | 2                               |
| 9.2    | Add semantic to parameters/properties | Could  | 2                               |
| 10.1   | Add heuristics                        | Could  | 2                               |
| 10.2   | Add log to failed tests               | Could  | 2                               |