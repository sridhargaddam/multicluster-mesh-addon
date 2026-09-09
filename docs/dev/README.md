# Development

## Documentation

- [environment.md](environment.md) - Development environment setup, building, deploying, running locally
- [design.md](design.md) - Architecture, design decisions, CRD internals
- [release-process.md](release-process.md) - Creating releases

## Getting Started

1. Read the [design document](design.md) to understand the architecture and design decisions.
2. Review the [contributing guide](../../CONTRIBUTING.md) for the PR process, DCO, and team conventions.
3. Set up a [development environment](environment.md).

## Running Tests

```bash
make verify                  # gofmt, modules, vet, istio-reader RBAC drift check
make test                    # unit tests
make test-integration        # integration tests (envtest - K8s cluster API running in memory)
make test-e2e                # e2e tests (requires a running development environment)
make test-e2e-multicluster   # multi-primary e2e tests (requires make dev-env)
```

For e2e tests, the addon must be deployed first (`make dev-env` or `make deploy`).
See [environment setup](environment.md) for options.
See [test/integration/README.md](../../test/integration/README.md) for test structure and adding CRDs.

`make verify` includes `make verify-istio-reader-rbac`, which fetches the upstream
Istio Helm templates and checks the embedded `pkg/hub/mesh/manifests/istio-reader-*.yaml`
for drift.
It requires network access; override the Istio ref it compares against with
`ISTIO_READER_REF` (default: `master`), or skip it in offline environments with
`ISTIO_READER_SKIP=1`.
