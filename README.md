Code to build the docker container ```eqtlbench``` and benchmark eQTL methods.

To build the container:
```
git clone https://github.com/tfguinan/eqtlbench
cd eqtlbench/container
# Build with correct Docker emulation, disabled provenance (allow singularity pull), and push to Docker Hub
docker buildx build --platform=linux/amd64 --provenance=false --push -t tfguinan/eqtlbench:0.1.0 .
```