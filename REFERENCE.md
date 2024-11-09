# Commands Reference


# Helm App life-cycle management:


* helm repo add stable https://charts.helm.sh/stable
* helm repo update
* helm repo list
* override default values provided by a chart: helm show values stable/mysql > my-values.yaml 
* install using custom values: helm install my-mysql -f my-values.yaml stable/mysql
* upgrade the release: helm upgrade my-mysql -f my-values.yaml stable/mysql

# Helm Chart Creation

* Generate boilerplate: helm create my-chart
* Add kubernetes manifests to the ./templates directory
* Package the chart: helm package my-chart
* install the chart: helm install my-release my-chart-<version>.tgz

# Helm Pre-install Hooks

```
apiVersion: batch/v1
kind: Job
metadata:
  name: "{{ .Release.Name }}-pre-install"
  labels:
    app: "{{ .Release.Name }}"
  annotations:
    "helm.sh/hook": pre-install
spec:
  template:
    spec:
      containers:
      - name: pre-install-job
        image: busybox
        command: ['sh', '-c', 'echo Hello from the pre-install hook!']
      restartPolicy: Never
```

# A skeleton Helm Charted Application


* https://github.com/devopsjourney1/helm-webapp
