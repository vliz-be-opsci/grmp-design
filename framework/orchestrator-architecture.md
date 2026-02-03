# Orchestrator architecture

1. Orchestrator in Python, uses [Docker SDK for Python](https://docker-py.readthedocs.io/en/stable/)
2. Reads the configuration file (YAML) and controls workers (= tests)
3. Each test that is run is a container that receives input parameters via the orchestrator (from
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