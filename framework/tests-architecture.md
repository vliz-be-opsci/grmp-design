# Tests architecture

1. Test is a container, pre-built image + tested via unit tests and offered via container registry (
   Dockerhub, Github Container registry, etc.).
2. Tests written by Sirus mainly in Python, but can be in any language/any framework.
3. Code used to build images (and run unit tests) is stored in a separate repository, ~~1
   test/repository~~, initially all Sirus-built tests will be in 1 repository.
4. Must be able to receive input from the orchestrator and produce Junit XML output according to an agreed format. 