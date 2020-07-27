# END Clothing Exercise

## Go live plan
- How the code build would works
The wordpress code, as well as the configuration (k8s and app specific) for Redis and MySQL, would reside in the same git repository. 

The code build would involve packaging php with the wordpress source code, and installing the extensions required for Wordpress (such as pdo-mysql).

- How the deployment would work
Reviews apps on every merge request to reduce bottleneck on the staging environment when multiple features are demo'd. 

Package with helm to facilitate rolling back the code as well as its configmaps and other dependencies in one command.

If HA is desired, we'd ideally be deployed to at least 3 different regions, each having their own k8s cluster. We'd ideally front the cluster-specific load balancers with a global load balancer meant to provide regional fail-over in case one regions goes down.

- How configuration and credentials would be passed to the application
Ideally, credentials wouldn't be passed from the application, but the application would retrieve it on start-up from something such as Vault by Hashicorp.

Configuration should be passed with a configmap.

- What monitoring you would put in place
Monitor your SLIs according to the SLA that has been published for the website (availability, latency, error rate).

Additionally, both Redis and MySQL's internal metrics can be easily exported to Prometheus.

The resource usage on the instance and k8s pods would also be monitored, but this would be set up globally on the cluster - you wouldn't set it up for each project.  

## Dockerfile and Kubernetes Configuration Files
Due to lack of time, none of the configuration files have been made to run as-is, but rather are meant to only serve as an example and discussion point for the final stage.

There's also a helm chart for wordpress, that I'd recommend using if a team asked me how they could deploy wordpress on their cluster. Similarly, bitnami maintains a chart for redis.
