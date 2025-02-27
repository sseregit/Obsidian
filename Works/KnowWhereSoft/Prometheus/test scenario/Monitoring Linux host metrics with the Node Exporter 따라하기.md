[Monitoring Linux host metrics with the Node Exporter](https://prometheus.io/docs/guides/node-exporter/)

[node_exporter-1.9.0.darwin-amd64.tar.gz](https://github.com/prometheus/node_exporter/releases/download/v1.9.0/node_exporter-1.9.0.darwin-amd64.tar.gz)
설치후
[[First steps 따라하기.#Mac amd64 이슈]] 

```
# NOTE: Replace the URL with one from the above mentioned "downloads" page.
# <VERSION>, <OS>, and <ARCH> are placeholders.
wget https://github.com/prometheus/node_exporter/releases/download/v<VERSION>/node_exporter-<VERSION>.<OS>-<ARCH>.tar.gz
tar xvfz node_exporter-*.*-amd64.tar.gz
cd node_exporter-*.*-amd64
./node_exporter
```