# Podman

Podman is a daemonless container engine for developing, managing, and running Open Container Initiative (OCI) containers and container images on your Linux System. Podman provides a Docker-compatible command line interface (CLI) that also supports the Open Container Initiative (OCI) specification. Podman is a part of the libpod library, which is a set of tools for managing containers and pods, including Podman, Buildah, Skopeo, and CRI-O.

Podman is designed to be a drop-in replacement for Docker, providing a similar user experience and feature set. However, Podman does not require a daemon to run containers, making it more lightweight and secure than Docker. Podman can run containers as a non-root user, which improves security by reducing the attack surface of the container runtime.

Podman is a powerful tool for building, running, and managing containers on Linux systems. It is well-suited for developers, system administrators, and anyone who needs to work with containers in a secure and efficient manner.

Podman key concept is usage of `Pods` which are groups of containers that share the same network and storage namespaces. Pods are useful for running multi-container applications that need to communicate with each other over the network or share storage volumes.

Yaml file is used to define the pod configuration. The Yaml file contains the configuration for the pod, including the containers that are part of the pod, the network and storage volumes they share, and other settings. The Yaml file can be used to create, manage, and delete pods using the `podman` command line interface.

```bash
podman generate kube myapp > myapp.yaml
```
