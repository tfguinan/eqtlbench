Code to build the docker container ```eqtlbench``` and benchmark eQTL methods.

To build the container:
```
git clone https://github.com/tfguinan/eqtlbench
cd eqtlbench/container
# Build using correct Docker emulation and disabled provenance to allow singularity pull
docker build --platform=linux/amd64 --provenance=false -t eqtlbench:0.1.0 .
```