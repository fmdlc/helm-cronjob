# helm-cronjob template
![](https://img.shields.io/github/last-commit/fmdlc/helm-cronjob)
![https://github.com/fmdlc/helm-cronjob/issues](https://img.shields.io/github/issues-raw/fmdlc/helm-cronjob)
![](https://img.shields.io/github/forks/fmdlc/helm-cronjob?style=plastic)
![https://github.com/fmdlc/helm-cronjob/blob/master/LICENSE](https://img.shields.io/github/license/fmdlc/helm-cronjob)

Helm Chart to define and run a Kubernetes scheduled task by defining a `cronjob` ojbect ☸.


```yaml
namespace: "default"
image:
  repository: alpine
  pullPolicy: IfNotPresent
  tag: 3.7
cron:
  restartPolicy: Never
  concurrencyPolicy: Forbid
  successfulJobsHistoryLimit: 2
  failedJobsHistoryLimit: 3
  schedule: "*/10 * * * *"
  parallelism: 1
  env:
  - name: DB_NAME
      value: "my_db"
  command: ["sleep"]
  args:
    - 10
resources:
  limits:
    cpu: 1
    memory: 200Mi
  requests:
    cpu: 0.5
    memory: 100Mi
nodeSelector: {}
tolerations: []
affinity: {}
```

## Usage
1) Edit `values.yaml` file in order to setup your environment.

2) First test installation with `--dry-run` parameter. You can specify the namespace by using `-n` modificator or alter any input parameter with `--set=<PARAMETER:VALUE>`.
3) If definition works as expected remove the `--dry-run` from the arguments.
```bash
$: helm install my-cronjob . --dry-run

NAME: my-cronjob
LAST DEPLOYED: Sun Aug 23 18:57:08 2020
NAMESPACE: default
STATUS: pending-install
REVISION: 1
TEST SUITE: None
HOOKS:
MANIFEST:
---
# Source: health-service/templates/cronjob.yaml
apiVersion: batch/v1beta1
kind: CronJob
...
```

## Contributing
Pull requests are welcome. For major changes, please open an issue first to discuss what you would like to change.

Please make sure to update tests as appropriate.

## License
[Apache 2.0](https://www.apache.org/licenses/LICENSE-2.0)
