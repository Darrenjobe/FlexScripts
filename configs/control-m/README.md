# Control-M Automation API – New Relic Flex Integration

This configuration uses [New Relic Flex](https://github.com/newrelic/nri-flex) to pull operational data from the [BMC Control-M Automation API](https://docs.bmc.com/docs/automation-api/) and send it to New Relic as custom events.

## Prerequisites

- New Relic Infrastructure agent installed and running.
- `nri-flex` installed (bundled with the Infrastructure agent v1.10.7+).
- A BMC Control-M environment with the Automation API enabled.
- A Control-M API user with appropriate read permissions.

## Configuration

1. Copy `flex-control-m-automation-api.yml` to the Flex configuration directory on your Infrastructure host (e.g. `/etc/newrelic-infra/integrations.d/`).
2. Replace the placeholder values in the file:
   - `<CONTROLM_HOST>` – hostname or IP of your Control-M/EM server.
   - `<CONTROLM_PORT>` – port of the Automation API gateway (default: `8443`).
   - `<CONTROLM_TOKEN>` – API token obtained from `POST /session/login`.
   - `<CONTROLM_SERVER>` – name of the Control-M Server to query (used for server-scoped endpoints).
3. Restart the New Relic Infrastructure agent.

### Obtaining an API Token

```bash
# For testing only – replace --cacert with your CA bundle in production
curl --cacert /path/to/ca-bundle.crt \
  -X POST "https://<CONTROLM_HOST>:<CONTROLM_PORT>/automation-api/session/login" \
  -H "Content-Type: application/json" \
  -d '{"username":"<user>","password":"<password>"}'
```

The response contains a `token` field. Use this value for `<CONTROLM_TOKEN>`.

> **Warning:** Do not use `-k` / `--insecure` with curl in production. Always verify the server certificate by providing the appropriate CA bundle via `--cacert`, or by ensuring the CA is trusted by the system.

## Data Collected

| Event Type | Description |
|------------|-------------|
| `ControlMJobStatusSample` | Status and details for all active/recent jobs |
| `ControlMAgentSample` | Status of Control-M Agents registered to the server |

## Notes

- The Automation API typically listens on HTTPS. If the server uses a self-signed certificate, configure the CA certificate on the Infrastructure host (or provide the `ca_file` path in `tls_config`) so that certificate verification succeeds. Setting `insecure_skip_verify: true` disables all TLS verification and should **never** be used in production.
- Adjust the `interval` value to suit your polling requirements.
