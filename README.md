# Instrumented Nginx Dockerfile
Nginx compiled with --with-stream to be able to create proxies or loadbalancers for non http protocols.

This repository contains **Dockerfile** of an instrumented version of Nginx for Prometheus

### Base Docker Image

* [alpine](https://hub.docker.com/_/alpine/)


### Installation

1. Install [Docker](https://www.docker.com/).

2. Download: `docker pull tekn0ir/nginx_prometheus`

(alternatively, you can build an image from Dockerfile:
```bash
$ docker build -t tekn0ir/nginx_prometheus github.com/tekn0ir/nginx_prometheus
```

### Usage
Start deamon
```bash
$ docker run -d -p 80:80 -p 9101:9101 --name nginx-prometheus tekn0ir/nginx_prometheus
```
Browse to http://localhost:9101/metrics and see the metrics scrapable by Prometheus

### Configure
Start deamon with configs mounted into `/etc/nginx/conf.d/`
```bash
$ docker run -d -p 80:80 -p 9101:9101 -v `pwd`/myconfig.conf:/etc/nginx/conf.d/myconfig.conf  --name nginx tekn0ir/nginx_prometheus
```
or to serve some html etc. directly:
```bash
$ docker run -d -p 80:80 -p 9101:9101 -v `pwd`/myhtml:/usr/share/nginx/html  --name nginx tekn0ir/nginx_prometheus
```
Browse to http://localhost:9101/metrics and see the metrics scrapable by Prometheus

### Metrics
You will see parts of or all of the prometheus output below:
```
# HELP nginx_http_connections Number of HTTP connections
# TYPE nginx_http_connections gauge
nginx_http_connections{state="active"} 1
nginx_http_connections{state="reading"} 0
nginx_http_connections{state="waiting"} 0
nginx_http_connections{state="writing"} 1
# HELP nginx_http_request_time HTTP request time
# TYPE nginx_http_request_time histogram
nginx_http_request_time_bucket{host="localhost",le="03.000"} 1
nginx_http_request_time_bucket{host="localhost",le="04.000"} 1
nginx_http_request_time_bucket{host="localhost",le="05.000"} 1
nginx_http_request_time_bucket{host="localhost",le="10.000"} 1
nginx_http_request_time_bucket{host="localhost",le="+Inf"} 1
nginx_http_request_time_bucket{host="testservers",le="00.005"} 1
nginx_http_request_time_bucket{host="testservers",le="00.010"} 1
nginx_http_request_time_bucket{host="testservers",le="00.020"} 1
nginx_http_request_time_bucket{host="testservers",le="00.030"} 1
nginx_http_request_time_bucket{host="testservers",le="00.050"} 1
nginx_http_request_time_bucket{host="testservers",le="00.075"} 1
nginx_http_request_time_bucket{host="testservers",le="00.100"} 1
nginx_http_request_time_bucket{host="testservers",le="00.200"} 1
nginx_http_request_time_bucket{host="testservers",le="00.300"} 1
nginx_http_request_time_bucket{host="testservers",le="00.400"} 1
nginx_http_request_time_bucket{host="testservers",le="00.500"} 1
nginx_http_request_time_bucket{host="testservers",le="00.750"} 1
nginx_http_request_time_bucket{host="testservers",le="01.000"} 1
nginx_http_request_time_bucket{host="testservers",le="01.500"} 1
nginx_http_request_time_bucket{host="testservers",le="02.000"} 1
nginx_http_request_time_bucket{host="testservers",le="03.000"} 1
nginx_http_request_time_bucket{host="testservers",le="04.000"} 1
nginx_http_request_time_bucket{host="testservers",le="05.000"} 1
nginx_http_request_time_bucket{host="testservers",le="10.000"} 1
nginx_http_request_time_bucket{host="testservers",le="+Inf"} 1
nginx_http_request_time_count{host="localhost"} 1
nginx_http_request_time_count{host="testservers"} 1
nginx_http_request_time_sum{host="localhost"} 2.0099999904633
nginx_http_request_time_sum{host="testservers"} 0
# HELP nginx_http_requests Number of HTTP requests
# TYPE nginx_http_requests counter
nginx_http_requests{host="localhost",status="200"} 1
nginx_http_requests{host="testservers",status="200"} 1
# HELP nginx_http_upstream_connect_time HTTP upstream connect time
# TYPE nginx_http_upstream_connect_time histogram
nginx_http_upstream_connect_time_bucket{addr="10.12.13.14:80",le="03.000"} 1
nginx_http_upstream_connect_time_bucket{addr="10.12.13.14:80",le="04.000"} 1
nginx_http_upstream_connect_time_bucket{addr="10.12.13.14:80",le="05.000"} 1
nginx_http_upstream_connect_time_bucket{addr="10.12.13.14:80",le="10.000"} 1
nginx_http_upstream_connect_time_bucket{addr="10.12.13.14:80",le="+Inf"} 1
nginx_http_upstream_connect_time_bucket{addr="127.0.0.1:80",le="00.005"} 1
nginx_http_upstream_connect_time_bucket{addr="127.0.0.1:80",le="00.010"} 1
nginx_http_upstream_connect_time_bucket{addr="127.0.0.1:80",le="00.020"} 1
nginx_http_upstream_connect_time_bucket{addr="127.0.0.1:80",le="00.030"} 1
nginx_http_upstream_connect_time_bucket{addr="127.0.0.1:80",le="00.050"} 1
nginx_http_upstream_connect_time_bucket{addr="127.0.0.1:80",le="00.075"} 1
nginx_http_upstream_connect_time_bucket{addr="127.0.0.1:80",le="00.100"} 1
nginx_http_upstream_connect_time_bucket{addr="127.0.0.1:80",le="00.200"} 1
nginx_http_upstream_connect_time_bucket{addr="127.0.0.1:80",le="00.300"} 1
nginx_http_upstream_connect_time_bucket{addr="127.0.0.1:80",le="00.400"} 1
nginx_http_upstream_connect_time_bucket{addr="127.0.0.1:80",le="00.500"} 1
nginx_http_upstream_connect_time_bucket{addr="127.0.0.1:80",le="00.750"} 1
nginx_http_upstream_connect_time_bucket{addr="127.0.0.1:80",le="01.000"} 1
nginx_http_upstream_connect_time_bucket{addr="127.0.0.1:80",le="01.500"} 1
nginx_http_upstream_connect_time_bucket{addr="127.0.0.1:80",le="02.000"} 1
nginx_http_upstream_connect_time_bucket{addr="127.0.0.1:80",le="03.000"} 1
nginx_http_upstream_connect_time_bucket{addr="127.0.0.1:80",le="04.000"} 1
nginx_http_upstream_connect_time_bucket{addr="127.0.0.1:80",le="05.000"} 1
nginx_http_upstream_connect_time_bucket{addr="127.0.0.1:80",le="10.000"} 1
nginx_http_upstream_connect_time_bucket{addr="127.0.0.1:80",le="+Inf"} 1
nginx_http_upstream_connect_time_count{addr="10.12.13.14:80"} 1
nginx_http_upstream_connect_time_count{addr="127.0.0.1:80"} 1
nginx_http_upstream_connect_time_sum{addr="10.12.13.14:80"} 2.006
nginx_http_upstream_connect_time_sum{addr="127.0.0.1:80"} 0
# HELP nginx_http_upstream_header_time HTTP upstream header time
# TYPE nginx_http_upstream_header_time histogram
nginx_http_upstream_header_time_bucket{addr="10.12.13.14:80",le="03.000"} 1
nginx_http_upstream_header_time_bucket{addr="10.12.13.14:80",le="04.000"} 1
nginx_http_upstream_header_time_bucket{addr="10.12.13.14:80",le="05.000"} 1
nginx_http_upstream_header_time_bucket{addr="10.12.13.14:80",le="10.000"} 1
nginx_http_upstream_header_time_bucket{addr="10.12.13.14:80",le="+Inf"} 1
nginx_http_upstream_header_time_bucket{addr="127.0.0.1:80",le="00.005"} 1
nginx_http_upstream_header_time_bucket{addr="127.0.0.1:80",le="00.010"} 1
nginx_http_upstream_header_time_bucket{addr="127.0.0.1:80",le="00.020"} 1
nginx_http_upstream_header_time_bucket{addr="127.0.0.1:80",le="00.030"} 1
nginx_http_upstream_header_time_bucket{addr="127.0.0.1:80",le="00.050"} 1
nginx_http_upstream_header_time_bucket{addr="127.0.0.1:80",le="00.075"} 1
nginx_http_upstream_header_time_bucket{addr="127.0.0.1:80",le="00.100"} 1
nginx_http_upstream_header_time_bucket{addr="127.0.0.1:80",le="00.200"} 1
nginx_http_upstream_header_time_bucket{addr="127.0.0.1:80",le="00.300"} 1
nginx_http_upstream_header_time_bucket{addr="127.0.0.1:80",le="00.400"} 1
nginx_http_upstream_header_time_bucket{addr="127.0.0.1:80",le="00.500"} 1
nginx_http_upstream_header_time_bucket{addr="127.0.0.1:80",le="00.750"} 1
nginx_http_upstream_header_time_bucket{addr="127.0.0.1:80",le="01.000"} 1
nginx_http_upstream_header_time_bucket{addr="127.0.0.1:80",le="01.500"} 1
nginx_http_upstream_header_time_bucket{addr="127.0.0.1:80",le="02.000"} 1
nginx_http_upstream_header_time_bucket{addr="127.0.0.1:80",le="03.000"} 1
nginx_http_upstream_header_time_bucket{addr="127.0.0.1:80",le="04.000"} 1
nginx_http_upstream_header_time_bucket{addr="127.0.0.1:80",le="05.000"} 1
nginx_http_upstream_header_time_bucket{addr="127.0.0.1:80",le="10.000"} 1
nginx_http_upstream_header_time_bucket{addr="127.0.0.1:80",le="+Inf"} 1
nginx_http_upstream_header_time_count{addr="10.12.13.14:80"} 1
nginx_http_upstream_header_time_count{addr="127.0.0.1:80"} 1
nginx_http_upstream_header_time_sum{addr="10.12.13.14:80"} 2.006
nginx_http_upstream_header_time_sum{addr="127.0.0.1:80"} 0.004
# HELP nginx_http_upstream_requests Number of HTTP upstream requests
# TYPE nginx_http_upstream_requests counter
nginx_http_upstream_requests{addr="10.12.13.14:80",status="504"} 1
nginx_http_upstream_requests{addr="127.0.0.1:80",status="200"} 1
# HELP nginx_http_upstream_response_time HTTP upstream response time
# TYPE nginx_http_upstream_response_time histogram
nginx_http_upstream_response_time_bucket{addr="10.12.13.14:80",le="03.000"} 1
nginx_http_upstream_response_time_bucket{addr="10.12.13.14:80",le="04.000"} 1
nginx_http_upstream_response_time_bucket{addr="10.12.13.14:80",le="05.000"} 1
nginx_http_upstream_response_time_bucket{addr="10.12.13.14:80",le="10.000"} 1
nginx_http_upstream_response_time_bucket{addr="10.12.13.14:80",le="+Inf"} 1
nginx_http_upstream_response_time_bucket{addr="127.0.0.1:80",le="00.005"} 1
nginx_http_upstream_response_time_bucket{addr="127.0.0.1:80",le="00.010"} 1
nginx_http_upstream_response_time_bucket{addr="127.0.0.1:80",le="00.020"} 1
nginx_http_upstream_response_time_bucket{addr="127.0.0.1:80",le="00.030"} 1
nginx_http_upstream_response_time_bucket{addr="127.0.0.1:80",le="00.050"} 1
nginx_http_upstream_response_time_bucket{addr="127.0.0.1:80",le="00.075"} 1
nginx_http_upstream_response_time_bucket{addr="127.0.0.1:80",le="00.100"} 1
nginx_http_upstream_response_time_bucket{addr="127.0.0.1:80",le="00.200"} 1
nginx_http_upstream_response_time_bucket{addr="127.0.0.1:80",le="00.300"} 1
nginx_http_upstream_response_time_bucket{addr="127.0.0.1:80",le="00.400"} 1
nginx_http_upstream_response_time_bucket{addr="127.0.0.1:80",le="00.500"} 1
nginx_http_upstream_response_time_bucket{addr="127.0.0.1:80",le="00.750"} 1
nginx_http_upstream_response_time_bucket{addr="127.0.0.1:80",le="01.000"} 1
nginx_http_upstream_response_time_bucket{addr="127.0.0.1:80",le="01.500"} 1
nginx_http_upstream_response_time_bucket{addr="127.0.0.1:80",le="02.000"} 1
nginx_http_upstream_response_time_bucket{addr="127.0.0.1:80",le="03.000"} 1
nginx_http_upstream_response_time_bucket{addr="127.0.0.1:80",le="04.000"} 1
nginx_http_upstream_response_time_bucket{addr="127.0.0.1:80",le="05.000"} 1
nginx_http_upstream_response_time_bucket{addr="127.0.0.1:80",le="10.000"} 1
nginx_http_upstream_response_time_bucket{addr="127.0.0.1:80",le="+Inf"} 1
nginx_http_upstream_response_time_count{addr="10.12.13.14:80"} 1
nginx_http_upstream_response_time_count{addr="127.0.0.1:80"} 1
nginx_http_upstream_response_time_sum{addr="10.12.13.14:80"} 2.006
nginx_http_upstream_response_time_sum{addr="127.0.0.1:80"} 0.004
# HELP nginx_metric_errors_total Number of nginx-lua-prometheus errors
# TYPE nginx_metric_errors_total counter
nginx_metric_errors_total 0
```