Find My Relative - Chart
========================

Helm chart for installing the Find My Relative application on an OpenShift cluster.


Prerequisites
-------------

- An OpenShift v4.x cluster
- OpenShift Pipelines Operator
- OpenShift Serverless Operator

Setting up webhooks
-------------------

GitHub webhooks can be used if you wish to trigger new deployments on commit pushes.
Webhooks can be set up manually using the GitHub website, or automated using a personal access token.

To set up webhooks, fork the [findmyrelative-frontend](https://github.com/Emergency-Response-Demo/findmyrelative-frontend) and [find-service](https://github.com/Emergency-Response-Demo/find-service) repositories, and update the corresponding values `frontend.github` and `backend.github` in `Values.yaml`.

### Using token:

1. Create a GitHub token, follow the instructions [here](https://help.github.com/en/github/authenticating-to-github/creating-a-personal-access-token-for-the-command-line#creating-a-token). This should be done for both the forked repositories.
2. Add the tokens to `frontend.token` and `backend.token`.
3. Install the chart.

### Manually:

1. Install the chart. Check the post-install message for instructions to get the listener URLs.
2. Create webhooks for the repositories, instructions [here](https://developer.github.com/webhooks/creating). Use the listener URLs for setting the payload URLs.
3. Install the chart.

Installing the Chart
--------------------

1. Create a new project:
   ```bash
   oc new-project find-my-relative
   ```

2. Modify `erdemo.incidentService` and `erdemo.missionService` in the `values.yaml` file with URLs of the Emergency Response Demo services.

   Set the `pipelines.start` value to `true` if the pipeline needs to be started immediately upon install.

   Alternatively, all the values may be specified using the `--set` parameter when installing.

3. Install the chart using `helm` cli:

   ```bash
   helm install <release-name> findmyrelative-chart [--tls]
   ```
