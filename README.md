[![Build Status](https://travis-ci.org/garethahealy/registry-ocp-monitoring.svg?branch=master)](https://travis-ci.org/garethahealy/registry-ocp-monitoring)
[![License](https://img.shields.io/hexpm/l/plug.svg?maxAge=2592000)]()

# registry-ocp-monitoring
## Disclaimer
**Supportability:**
*If you are a RedHat customer; it is __suggested__ you raise a support ticket to clarify the supportability of the below components.
The below are the views of my own, and not representative of RedHat nor of any communities mentioned.*
- Hawkular OpenShift Agent is only supported [upstream](http://www.hawkular.org/community/docs/getting-involved/)
- CoreOS Registry Monitor is only supported [upstream](https://github.com/coreos/registry-monitor/issues)
- Hawkular Grafana DataSource is only supported [upstream](https://github.com/hawkular/hawkular-grafana-datasource/issues)

## Preface
This blog post is a continuation of [FIS2.0 OCP Monitoring via Hawkular OpenShift Agent](https://github.com/garethahealy/fis2-ocp-monitoring). 
Before continuing; it is expected you have deployed the Hawkular OpenShift Agent and monitoring an example application. 

### Scenario
todo

### Solution
- https://github.com/coreos/registry-monitor

## Example Deployment
### ...
pull image

    docker pull docker.io/centos:7

create project

    oc new-project registry-monitoring

create configmap for settings

    oadm policy add-scc-to-user privileged system:serviceaccount:registry-monitoring:registry-monitor

    REGISTRY_SVC_IP=$(oc get svc docker-registry -n default -o jsonpath='{.spec.clusterIP}')
    USER_TOKEN=$(oc whoami -t)
    oc process -f https://raw.githubusercontent.com/garethahealy/registry-ocp-monitoring/master/ocp-template/registry-monitor-config.yaml REGISTRY_SVC_IP=$REGISTRY_SVC_IP PASSWORD=$USER_TOKEN | oc create -f -

create pod

    oc process -f https://raw.githubusercontent.com/garethahealy/registry-ocp-monitoring/master/ocp-template/registry-monitor.yaml | oc create -f -

## Conclusion
todo

### Whats next?
todo
