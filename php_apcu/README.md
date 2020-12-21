# Agent Check: php_apcu

## Overview

This check monitors [PHP APCu][1] through the Datadog Agent.

## Setup

Follow the instructions below to install and configure this check for an Agent running on a host. For containerized environments, see the [Autodiscovery Integration Templates][2] for guidance on applying these instructions.

### Installation

To install the `php_apcu` check on your host:


1. Install the [developer toolkit][3].
 on any machine.

2. Run `ddev release build php_apcu` to build the package.

3. [Download the Datadog Agent][4].

4. Upload the build artifact to any host with an Agent and
 run `datadog-agent integration install -w
 path/to/php_apcu/dist/<ARTIFACT_NAME>.whl`.

#### APCu Setup


APCu does not expose metrics by default so this integration includes a metric exporter, located here:

```
/opt/datadog-agent/embedded/lib/python3.8/site-packages/datadog_checks/php_apcu/assets/exporter/apcu-dd-handler.php
```
you can download [here][5].

When you configure your Agent (the `instances` setting, described next), you can refer to the exporter directly. by this file name, or you can configure an alias for it on your web server. For example, if you're using Apache, the alias in the web server configuration file would look like this:

```
Alias /apcu-status /opt/datadog-agent/embedded/lib/python3.8/site-packages/datadog_checks/php_apcu/assets/exporter/apcu-dd-handler.php
<Location /apcu-status>
    Require all denied
    Require local
</Location>
```

### Configuration

1. Edit the `php_apcu.d/conf.yaml` file, in the `conf.d/` folder at the root of your Agent's configuration directory to start collecting your `php_apcu` performance data. See the [sample `php_apcu.d/conf.yaml` file][6] for all available configuration options.
    ```
    instances
      - url: http://localhost/apcu-status
    ```
2. [Restart the Agent][7].

### Validation

[Run the Agent's status subcommand][8] and look for `php_apcu` under the Checks section.

## Data Collected

### Metrics

See [metadata.csv][9] for a list of metrics provided by this check.

### Service Checks

`php_apcu` does not include any service checks.

### Events

`php_apcu` does not include any events.

## Troubleshooting

Need help? Contact [Datadog support][10].

[1]: https://www.php.net/manual/en/book.apcu.php
[2]: https://docs.datadoghq.com/agent/kubernetes/integrations/
[3]: https://docs.datadoghq.com/developers/integrations/new_check_howto/#developer-toolkit
[4]: https://app.datadoghq.com/account/settings#agent
[5]: https://github.com/DataDog/integrations-extras/blob/master/php_apcu/datadog_checks/php_apcu/assets/exporter/apcu-dd-handler.php
[6]: https://github.com/DataDog/integrations-extras/blob/master/php_apcu/datadog_checks/php_apcu/data/conf.yaml.example
[7]: https://docs.datadoghq.com/agent/guide/agent-commands/#start-stop-and-restart-the-agent
[8]: https://docs.datadoghq.com/agent/guide/agent-commands/#agent-status-and-information
[9]: https://github.com/DataDog/integrations-extras/blob/master/php_apcu/metadata.csv
[10]: https://docs.datadoghq.com/help/
