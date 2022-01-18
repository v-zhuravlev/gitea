# Gitea Mixin

This mixin provides the Grafana dashboard with metrics exposed by Gitea, including application's key stats as well as CPU, memory, file descriptors utilization.


![image](https://storage.googleapis.com/grafanalabs-integration-assets/gitea/screenshots/screenshot0.png)

## Gitea configuration

To get metrics from Gitea instance you need to configure [metrics](https://docs.gitea.io/en-us/config-cheat-sheet/#metrics-metrics) section to enable /metrics endpoint:

```ini
[metrics]
ENABLED=true
```

In order to see issues stats grouped by repositores and labels, Gitea 1.16.0 or above is required with the following flags set:

```ini
[metrics]
ENABLED=true
ENABLED_ISSUE_BY_REPOSITORY=true
ENABLED_ISSUE_BY_LABEL=true
```

## Generate config files

You can manually generate dashboards, but first you should install some tools:

```bash
go install github.com/jsonnet-bundler/jsonnet-bundler/cmd/jb@latest
go install github.com/google/go-jsonnet/cmd/jsonnet@latest
# or in brew: brew install go-jsonnet
```

For linting and formatting, you would also need `mixtool` and `jsonnetfmt` installed. If you
have a working Go development environment, it's easiest to run the following:

```bash
go install github.com/monitoring-mixins/mixtool/cmd/mixtool@latest
go install github.com/google/go-jsonnet/cmd/jsonnetfmt@latest
```

The files in `dashboards_out` need to be imported
into your Grafana server.  The exact details will be depending on your environment.

Edit `config.libsonnet` if required and then build JSON dashboard files for Grafana:

```bash
make
```

For more advanced uses of mixins, see
https://github.com/monitoring-mixins/docs.
