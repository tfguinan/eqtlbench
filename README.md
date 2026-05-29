Code to build the docker container ```eqtlbench``` and benchmark eQTL methods.

To build the container:
```
git clone github.com/tfguinan/eqtlbench
cd eqtlbench/container
# Build using correct Docker emulation
docker build --platform=linux/amd64 -t qtlbench:0.1.0 .
```