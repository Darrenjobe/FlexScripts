# FlexScripts
A collection of custom configurations for [New Relic Flex](https://github.com/newrelic/nri-flex) (nri-flex).

These configurations are modeled after the [official nri-flex examples](https://github.com/newrelic/nri-flex/tree/master/examples) and are organized by solution.

## Directory Structure

```
configs/
└── control-m/    # BMC Control-M Automation API integration
```

## Usage

Each subdirectory under `configs/` contains a `README.md` with solution-specific setup instructions and one or more Flex YAML configuration files.

Copy the desired YAML file(s) to the `flexConfigs` directory on your New Relic Infrastructure host (typically `/etc/newrelic-infra/integrations.d/` or your Flex config path), then restart the Infrastructure agent.
