Find My Relative - Chart
========================

Helm chart for installing the Find My Relative application on an OpenShift cluster.


Prerequisites
-------------

- An OpenShift v4.x cluster
- OpenShift Pipelines Operator
- OpenShift Serverless Operator


Installing the Chart
--------------------

This chart does not create a new project for the application. Make sure that you are in the correct project before installing.

1. Modify `erdemo.incidentService` and `erdemo.missionService` in the `values.yaml` file with URLs of the Emergency Response Demo services.

   Set the `pipelines.start` value to `true` if the pipeline needs to be started immediately upon install.

   Alternatively, all the values may be specified using the `--set` parameter when installing.

2. Install the chart using `helm` cli:

   ```bash
   helm install <release-name> findmyrelative-chart [--tls]
   ```
