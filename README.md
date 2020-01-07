Find My Relative - Chart
========================

Helm chart for installing the Find My Relative application on an OpenShift cluster.


Prerequisites
-------------

- Requires OpenShift v4.x cluster
- OpenShift Pipelines Operator
- OpenShift Serverless Operator

Chart details
-------------

This chart installs the following:
- Pipeline that builds and deploys [findmyrelative-frontend](https://github.com/Emergency-Response-Demo/findmyrelative-frontend).
- Pipeline that builds and deploys [find-service](https://github.com/Emergency-Response-Demo/find-service).
- Event listeners for the applications that listen to GitHub webhook events, triggering the pipelines on code pushes.

Installation
--------------------

### Setting up webhooks

GitHub webhooks can be used if you wish to trigger the pipelines on code pushes.

Webhooks can either be set up manually on the GitHub website, or automated using a personal access token.

To set up webhooks, first fork the [findmyrelative-frontend](https://github.com/Emergency-Response-Demo/findmyrelative-frontend) and [find-service](https://github.com/Emergency-Response-Demo/find-service) repositories, and update the corresponding `frontend` and `backend` values in `Values.yaml`:

|Parameter    |Description                                                           |
|:-----------:|----------------------------------------------------------------------|
|`github.repo`|Name of the repository                                                |
|`github.user`|GitHub username                                                       |
|`github.org` |Organization name. If there is no org, replace with username          |
|`token`      |GitHub personal access token. Leave empty if setting webhooks manually|
|`secret`     |Random string for creating secrets                                    |

#### Using token:

1. Create a GitHub token, follow the instructions [here](https://help.github.com/en/github/authenticating-to-github/creating-a-personal-access-token-for-the-command-line#creating-a-token). This should be done for both the forked repositories.
2. Add the tokens to `frontend.token` and `backend.token`.
3. Install the chart.

#### Manually:

1. Install the chart first. Check the post-install message for instructions to get the event listener URLs.
2. Create webhooks for the repositories, instructions [here](https://developer.github.com/webhooks/creating). Use the listener URLs for setting the payload URLs.

## Installing the Chart

1. Create a new project:
   ```bash
   oc new-project find-my-relative
   ```

2. Set the following configuration options, you can edit the `Values.yaml` file, pass your own config file using `-f`, or use `--set` to specify the values directly.


|Parameter               |Description                                                                                                          |
|:----------------------:|---------------------------------------------------------------------------------------------------------------------|
|`erdemo.incidentService`|URL of incident service from the Emergency Response Demo applicaiton                                                 |
|`erdemo.missionService` |URL of mission service from the Emergency Response Demo applicaiton                                                  |
|`clusterHostname`       |External hostname of the cluster, used for determining `Route` URLs. Must be of the form `apps.<cluster-id>.<domain>`|
|`mapboxToken`           |Mapbox token for creating maps. Can be created [here](https://account.mapbox.com)                                    |
|`pipelines.start`       |Boolean value. Specifies wether the pipelines should start immediately upon install                                  |

3. Install the chart using `helm` cli:

   ```bash
   helm install <my-release> findmyrelative-chart [--tls]
   ```

## Verifying install

To verify the install or get status:
```bash
helm status <my-release> [--tls]
```

## Uninstallation
To uninstall/delete the application:
```bash
helm uninstall <my-release> [--tls]
```
