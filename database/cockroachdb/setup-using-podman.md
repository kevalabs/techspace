## Setup Cockroachdb using Podman

### Step 1: Prepare Certificate Directory
```bash
mkdir -p ~/cockroach-secure/certs
cd ~/cockroach-secure/certs
```

### Step 2: Generate TLS Certificates

```bash

# Create CA cert
podman run --rm -v "$(pwd)":/certs cockroachdb/cockroach:latest-v25.2 cert create-ca \
  --certs-dir=/certs --ca-key=/certs/ca.key

# Create node cert (for localhost access)
podman run --rm -v "$(pwd)":/certs cockroachdb/cockroach:latest-v25.2 cert create-node \
  localhost 127.0.0.1 cockroachdb \
  --certs-dir=/certs --ca-key=/certs/ca.key

# Create client cert for root
podman run --rm -v "$(pwd)":/certs cockroachdb/cockroach:latest-v25.2 cert create-client \
  root --certs-dir=/certs --ca-key=/certs/ca.key

```
### 📦 3. Create Podman Volume for Data
```bash
podman volume create cockroach-data

```
### 🚀 Step 4: Start CockroachDB (Secure, Full Mode)
```bash
podman run -d \
  --name cockroachdb \
  -p 26257:26257 \
  -p 8080:8080 \
  -v cockroach-data:/cockroach/cockroach-data \
  -v $(pwd):/cockroach/cockroach-certs:Z \
  docker.io/cockroachdb/cockroach:latest-v25.2 start \
  --certs-dir=/cockroach/cockroach-certs \
  --listen-addr=0.0.0.0:26257 \
  --http-addr=0.0.0.0:8080 \
  --advertise-addr=localhost \
  --join=localhost \
  --store=/cockroach/cockroach-data

```

### 🛠️ Step 5: Initialize the Cluster
```bash
podman exec -it cockroachdb ./cockroach init \
  --certs-dir=/cockroach/cockroach-certs \
  --host=localhost
```
### 🔐 Step 6: Set Password for root User
```bash
podman exec -it cockroachdb ./cockroach sql \
  --certs-dir=/cockroach/cockroach-certs \
  --host=localhost \
  -e "ALTER USER root WITH PASSWORD 'Root@786';"
```

### 🧪 Step 7: Verify Web UI Access
Open in browser:
📍 https://localhost:8080
  - Username: root
  - Password: Root@786
  - Accept the browser certificate warning
 
