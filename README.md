# IMPORtANT
This method is currentley not working with Traefik 2.2
You should deploy Traefik and after it was started successfully deploy the needed IngressRoute.  
Otherwise letsencrypt certificate generation will fail.

See [this terraform script](https://github.com/v-braun/aks-jump-starter/blob/master/helm.tf) that deploy the official Traefik Helm Chart and additionally the IngressRoute and middleware.



# Traefik Helm Chart with Dashboard

This Helm Chart is based on the [official Traefk Chart](https://github.com/containous/traefik-helm-chart), but add also an ``IngressRoute` and a `Midleware` for the Traefik Dashboard to make it public available

## Installation

```shell
helm repo add vbr https://raw.githubusercontent.com/v-braun/traefik-helm-chart/master/
helm repo update
helm install traefik vbr/vbr-traefik
```

### Configuration

```yaml
# public host for the dashboard
publicHost: dashboard.your-domain.here
ingressRoute: 
  # additional annotations that should be added to the ingress route
  annotations: {}
  # additional labels that should be added to the ingress route
  labels: {}
# secret used for basic auth
# secret should be generated with htpaswd (user:hashedpassword)
authSecretName: "my secret"

# entry points that the dashboard should be available on
entryPoints:
  - web
  - websecure

# configure here the main traefik chart values
# see here: https://github.com/containous/traefik-helm-chart/blob/master/traefik/values.yaml
# 
# traefik:
#   ...

```

## Develop
After changes in this repo, the following steps should be executed:  

1. Increase the version number in `Chart.yaml`
2. Package the Chart
```
helm package .
```
3. Index the repo
``` shell
helm repo index .
```



## Authors

![image](https://avatars3.githubusercontent.com/u/4738210?v=3&amp;s=50)  
[v-braun](https://github.com/v-braun/)



## Contributing

Make sure to read these guides before getting started:
- [Contribution Guidelines](https://github.com/v-braun/traefik-helm-chart/blob/master/CONTRIBUTING.md)
- [Code of Conduct](https://github.com/v-braun/traefik-helm-chart/blob/master/CODE_OF_CONDUCT.md)

## License
**traefik-helm-chart** is available under the MIT License. See [LICENSE](https://github.com/v-braun/traefik-helm-chart/blob/master/LICENSE) for details.

