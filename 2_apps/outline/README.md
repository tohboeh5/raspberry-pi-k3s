# Outline

## develop

```bash
kubectl create secret generic outline-secret -n outline --dry-run=client --from-env-file=.env --output=yaml > main/secret.yaml
```

```bash
kubectl apply -f init
kubectl apply -f main
```

~ $ ls -l datastores/uploads/dc918fe1-d840-4946-bbee-d971a4fd04b4/
total 28
drwxr-xr-x    2 root     root          4096 Mar 25 14:59 10ca45e3-8573-41c6-9cdd-45424c476e2e
drwxr-xr-x    2 root     root          4096 Mar 25 14:59 1869a9e1-af16-4c71-ae7a-fd2acc8a82b2
drwxr-xr-x    2 root     root          4096 Mar 25 14:59 6a31abc2-7e8b-44ed-925e-06a3a4d6444d
drwxr-xr-x    2 root     root          4096 Mar 25 14:59 6e9f208a-72a1-4d04-8b48-40b63c531d25
drwxr-xr-x    2 root     root          4096 Mar 25 14:59 961922e5-67a5-4158-86ca-5105bb209735
drwxr-xr-x    2 root     root          4096 Mar 25 14:59 a97027f4-6cd2-4e30-967a-ac6d3c558648
drwxr-xr-x    2 root     root          4096 Mar 25 14:59 c2eab2a6-6450-4acf-9ff7-b8b31ebf8fb1
