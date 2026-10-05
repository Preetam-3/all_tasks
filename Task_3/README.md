# Task 3 — Terraform + Docker

Terraform configuration that pulls the Ubuntu image and runs it as a container.

## Resources

| Resource | Type | Name | Notes |
| --- | --- | --- | --- |
| `docker_image.ubuntu` | `kreuzwerker/docker` | `ubuntu:latest` | Pulls the latest Ubuntu image |
| `docker_container.foo` | `kreuzwerker/docker` | `foo` | Runs the image above |

The provider talks to Docker over the local socket: `unix:///var/run/docker.sock`.

## Requirements

- Terraform
- A running Docker daemon reachable at `/var/run/docker.sock`
- Provider `kreuzwerker/docker` version `4.6.0` (see `.terraform.lock.hcl`)

## Usage

```sh
terraform init      # download the docker provider
terraform plan      # preview the image pull + container
terraform apply     # create the resources
```

Inspect the running container:

```sh
docker ps
docker exec -it foo bash
```

Tear everything down:

```sh
terraform destroy
```

## Files

- `main.tf` — provider and resource definitions
- `.terraform.lock.hcl` — pinned provider versions (commit this)
- `terraform.tfstate` — current state (**do not** commit; may contain secrets)
- `.terraform/` — provider binaries and module cache (do not commit)
