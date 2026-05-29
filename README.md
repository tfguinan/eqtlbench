Code to build the docker container ```eqtlbench``` and benchmark eQTL methods.

To build the container I ran:
```
git clone https://github.com/tfguinan/eqtlbench
cd eqtlbench/container
# Build with correct Docker emulation, disabled provenance (allow singularity pull), and push to Docker Hub
docker buildx build --platform=linux/amd64 --provenance=false --push -t tfguinan/eqtlbench:0.1.0 .
```

To run on HPC you run:
```
module load singularity/3.4.1
singularity pull docker://tfguinan/eqtlbench:0.1.0
# Check method versions
singularity exec eqtlbench_0.1.0.sif Rscript -e "library(MatrixEQTL); packageVersion('MatrixEQTL')"
singularity exec eqtlbench_0.1.0.sif bash -c "CONDA_OVERRIDE_GLIBC=2.28 pixi run R -e 'library(SAIGEQTL); packageVersion(\"SAIGEQTL\")'"
singularity exec eqtlbench_0.1.0.sif python -c "import memento; print(memento.__version__)"
```