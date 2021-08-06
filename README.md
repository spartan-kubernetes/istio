# Istio Config Repo

## Istio Installation

### First: Install Istio
Please follow these guidelines to install Istio through its Operator: https://istio.io/latest/docs/setup/install/operator/.
It will use the file `` istio-operator.yaml`` to deploy the Istio components within the cluster.

> Keep in mind: This yaml file, will deploy Istio Ingress Gateway as NodePort since
> AWS by default creates a Classic LoadBalancer, which should not be used for production
> grade applications (ALB and NLB are the ones suggested by AWS on its documentation).

### Second: Enable ALB Controller
Since the Istio Ingress Gateway is installed as NodePort, we need to tell to the ALB
Ingress Controller to redirect the incoming traffic to the Istio Ingress Gateway.
To do so, we must deploy the file `` istio-alb.yaml``, which will create an AWS ALB.

> Keep in mind: the AWS LoadBalancer Controller must be installed within the cluster
> to achieve this feature working.

### Third: Install Add-Ons
The tools that should be deployed once Istio is up and running are:

1. _**Kiali dashboard**_: https://istio.io/latest/docs/ops/integrations/kiali/
2. _**Jaegger tracing**_: https://istio.io/latest/docs/ops/integrations/jaeger/
3. _**Prometheus Monitoring**_: https://istio.io/latest/docs/ops/integrations/prometheus/
4. _**Grafana dashboard**_: https://istio.io/latest/docs/ops/integrations/grafana/

> More integrations can be found here: https://istio.io/latest/docs/ops/integrations/

### Fourth: Integration with Ingress Controller
Once those are deployed and running, in order to accept external traffic we can deploy one of these ingress configurations, 
depending on which Ingress Controller is running in the cluster.

1. For Nginx Ingress Controller: `` istio-nginx-ingress.yaml``