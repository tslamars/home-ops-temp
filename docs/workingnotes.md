## Troubleshooting

1. Verify the Git Repository is up-to-date and in a ready state.

    ```sh
    flux get sources git -A
    ```

    Force Flux to sync your repository to your cluster:

    ```sh
    flux -n flux-system reconcile ks flux-system --with-source
    ```

2. Verify all the Flux kustomizations are up-to-date and in a ready state.

    ```sh
    flux get ks -A
    ```

3. Verify all the Flux helm releases are up-to-date and in a ready state.

    ```sh
    flux get hr -A
    ```

4. Do you see the pod of the workload you are debugging?

    ```sh
    kubectl -n <namespace> get pods -o wide
    ```

5. Check the logs of the pod if its there.

    ```sh
    kubectl -n <namespace> logs <pod-name> -f
    ```

6. If a resource exists try to describe it to see what problems it might have.

    ```sh
    kubectl -n <namespace> describe <resource> <name>
    ```

7. Check the namespace events

    ```sh
    kubectl -n <namespace> get events --sort-by='.metadata.creationTimestamp'
    ```

- Bootstrap prerequisites

```
export ROOK_DISK=CT1000P3PSSD8
eval ($op signin)
```

- Debug task failure
```bash
minijinja-cli talos/controlplane.yaml.j2 | op inject
minijinja-cli bootstrap/resources.yaml.j2 | op inject
```
- Placeholder

```
  install:
    {% if node == "10.10.5.170" %}
    diskSelector:
      model: "ZETTASTONE CP200 1024GB"
    {% elif node == "10.10.5.171" %}
    diskSelector:
      model: "SAMSUNG MZ7TN512"
    {% elif node == "10.10.5.172" %}
    diskSelector:
      model: "Samsung SSD 860"
    {% else %}
    disk: /dev/sdb  # Fallback to a default path
    {% endif %}    
```