# Configs

This directory contains custom [New Relic Flex](https://github.com/newrelic/nri-flex) (nri-flex) configurations organized by solution.

## Solutions

| Directory | Description |
|-----------|-------------|
| [control-m](./control-m/) | BMC Control-M Automation API integration |

## Adding a New Solution

1. Create a new subdirectory named after the solution (e.g. `my-solution/`).
2. Add a `README.md` in the new subdirectory explaining prerequisites, configuration, and usage.
3. Add one or more Flex YAML configuration files following the [nri-flex configuration format](https://github.com/newrelic/nri-flex/blob/master/docs/basic-tutorial.md).
