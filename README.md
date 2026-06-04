# Rsync CAI Runtime (Python 3.12)

A custom [Cloudera AI](https://docs.cloudera.com/machine-learning/) (CAI) / Cloudera Data Science Workbench ML runtime based on the official **Python 3.12 JupyterLab (PBJ)** standard image, with **`rsync`** installed for file synchronization from sessions, jobs, and applications.

Use this runtime when workloads need `rsync` at the container level (for example, syncing project files or data to remote hosts) without installing it on every project startup.

## Published image

The image is published on Docker Hub:

| Registry | Image | Tag |
|----------|--------|-----|
| Docker Hub | `kevintalbert/rsyncruntime` | `latest` |

**Pull:**

```bash
docker pull docker.io/kevintalbert/rsyncruntime:latest
```

**Full reference:** `docker.io/kevintalbert/rsyncruntime:latest`

## What’s in the image

| Item | Value |
|------|--------|
| Base | `cloudera/cdsw/ml-runtime-pbj-jupyterlab-python3.12-standard:2026.01.1-b6` |
| Edition | `Rsync` (`ML_RUNTIME_EDITION` / `com.cloudera.ml.runtime.edition`) |
| Added packages | `rsync` (via `apt`) |

The Dockerfile extends the Cloudera base image only to install `rsync` and ship third-party notices; kernels, editors, and the rest of the standard Python 3.12 JupyterLab stack come from the base runtime.

## Register in Cloudera AI

Site administrators add the image in the **Runtime Catalog** (see [Add the new ML Runtime](https://docs.cloudera.com/cdsw/1.10.5/runtimes/topics/ml-registering-customized-runtimes.html)):

1. Open **Runtime Catalog** → **Add Runtime**.
2. Enter the image URL, for example: `docker.io/kevintalbert/rsyncruntime:latest`
3. Click **Validate**, then save if validation succeeds.

Custom runtimes must use a unique **Edition** name compared to Cloudera-built runtimes; this image sets Edition to **`Rsync`**.

For private registries, configure Docker credentials in CAI before validation. Public Docker Hub images typically need no extra credentials.

## Build from source

Requires access to the Cloudera base image registry (`docker.repository.cloudera.com`) and a logged-in Docker client where that registry is available.

```bash
git clone https://github.com/kevinbtalbert/Rsync-CAI-Runtime-Python-3.12.git
cd Rsync-CAI-Runtime-Python-3.12

docker build -t rsyncruntime:local .

# Optional: tag and push to your own registry
docker tag rsyncruntime:local docker.io/<your-user>/rsyncruntime:latest
docker push docker.io/<your-user>/rsyncruntime:latest
```

## Verify rsync

After the runtime is available in a session or job:

```bash
rsync --version
which rsync
```

## License and notices

- Project license: [Apache License 2.0](LICENSE)
- Third-party attributions for the runtime image: [third-party-notices.txt](third-party-notices.txt) (copied into the image at `/notices/NOTICE.txt`)

## References

- [Customized Runtimes](https://docs.cloudera.com/machine-learning/cloud/runtimes/topics/ml-customized-runtimes.html)
- [Distribute the ML Runtime image](https://docs.cloudera.com/machine-learning/1.5.5/managing-runtimes/topics/ml-distribute-the-runtime-image.html)
