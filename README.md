# Docker monitoring tools

Prerequisites: `docker` and `docker-compose`

To deploy everything locally run: `docker-compose -f docker-compose-collect.yml -f docker-compose-viz.yml -f docker-compose-openhim-test.yml up`

Then, access the UIs:

* Grafana: <http://localhost:3000> (u: admin, p: dev_password_only)
* OpenHIM: <http://localhost:9000> (u: root@openhim.org, p: openhim-password)
* Prometheus targets: <http://localhost:9090/targets>

A postman collection is included to send some test transactions, this will require that you import the channels and client from the `openhim-rw-test.json` export file into the OpenHIM.

The applications are split into separate compose files so they may be deployed separately, these are:

* `docker-compose-collect.yml` - to run the metrics collection tools. Should be run on the server to be observed.
* `docker-compose-viz.yml` - to run the visualisation tools, Prometheus and Grafana, make sure the `prometheus.yml` file is updated so that the targets to point to the location of the collection tools. See, `prometheus-remote.yml`.
* `docker-compose-openhim-test.yml` - to run the OpenHIM easily for testing purposes.

The OpenHIM will need to upgraded to version `v8.1.1` for the prometheus exporter endpoint to be available.

Currently, the previous version of the collection tools are running on the Rwanda HIE Productions server and viz tools are running on a test server separately to reduce load on the production server.
