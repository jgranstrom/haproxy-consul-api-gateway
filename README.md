# HAproxy consul API gateway

Preconfigured setup for an API gateway using consul service discovery to discover API instances.

This will look at the tags of your services registered with consul and proxy all services that includes the tag `api` automatically.

If you are running [registrator](https://github.com/gliderlabs/registrator) this means including an environment variable `SERVICE_TAGS=api`.

All API services will be exposed on their own frontend and loadbalanced between running instances. Each service will be exposed on a path like `<haproxy-host>/api/<service_name>[additional_path]` and rewritten to `<service_instance_ip>:<service_instance_port>[additional_path]`.

So if you have a service registered on consul with the name `my-service` with a path `/ping` it will be accessible through HAProxy at `http://<haproxy-host>/api/my-service/ping`.

## Usage
```
docker run -p 8080:80 jgranstrom/haproxy-consul-api-gateway
```
