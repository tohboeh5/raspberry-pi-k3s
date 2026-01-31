# Immich

## deploy

### 1) prerequisites

- Sealed Secrets controller is installed.
- CloudNativePG operator is installed.

### 2) create the SealedSecret

```bash
kubectl create secret generic immich-db -n immich \
	--from-env-file=.env \
	--dry-run=client -o yaml | \
	kubeseal \
		--controller-name=sealed-secrets \
		--controller-namespace=kube-system \
		--format=yaml > main/immich-sealed-secrets.yaml
```


### 3) apply base resources

```bash
kubectl create namespace immich || true
kubectl apply -f init
kubectl apply -f main/postgres.yaml
kubectl apply -f main/immich-sealed-secrets.yaml
```

### 4) install/upgrade Immich with Helm

```bash
helm upgrade --install --create-namespace --namespace immich immich \
	oci://ghcr.io/immich-app/immich-charts/immich \
	-f main/immich-values.yaml
```

### notes

- Update `controllers.main.containers.main.image.tag` in [2_apps/immich/main/immich-values.yaml](2_apps/immich/main/immich-values.yaml) to pin the Immich version.
- `immich-postgres` uses the VectorChord-enabled CNPG image. Keep `shared_preload_libraries` and `postInitSQL` aligned with Immich docs.
