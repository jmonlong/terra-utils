# Eraser notebook

To clean up a workspace of temporary files. 

It helps understand how much space is used in the workspace, and assists in erasing the files you don't want to keep. 
It can erase files selected by size, date, extension while protecting those in the workspace's Tables or in specific submissions.

See [Eraser.ipynb](Eraser.ipynb) (some outputs with too much details are not shown).

# Custom notebook Docker container

This image extends the [terra-jupyter-r](https://github.com/DataBiosphere/terra-docker/blob/master/terra-jupyter-r/README.md) notebook with:

- [bcftools](https://samtools.github.io/bcftools/bcftools.html)
- [samtools](samtools.github.io/)
- [vg](https://github.com/vgteam/vg)
- [odgi](https://github.com/pangenome/odgi)
- `less` (!!!)
- GNU time (use with `env time` or `/usr/local/bin/time`)
- R packages:
    - [sveval](https://github.com/jmonlong/sveval) and its dependencies (inc. dplyr, ggplot2, BioC GenomicsRanges, VariantAnnotation)
- Python packages: `pysam`, `pyfaidx`, `biopython`, `cyvcf2`

## Build and push to DockerHub

Terra only accepts containers hosted on Google, GitHub, or DockerHub for its interactive environments (see [Terra support](https://support.terra.bio/hc/en-us/community/posts/4405150565659--Error-creating-cloud-environment-when-using-Quay-Docker-images-for-custom-cloud-environments)).
I just have a free account on DockerHub so I build the (big) image locally and push.

The DockerHub page is [jmonlong/terra-noteboook-custom](https://hub.docker.com/repository/docker/jmonlong/terra-noteboook-custom/general).

The latest version is `jmonlong/terra-notebook-custom:0.0.3`

```sh
docker build -t jmonlong-terra-notebook-custom .

docker tag jmonlong-terra-notebook-custom jmonlong/terra-notebook-custom:0.0.3
docker push jmonlong/terra-notebook-custom:0.0.3
```

## Run locally

```sh 
docker run --rm -it -p 8000:8000 jmonlong-terra-notebook-custom
```

Then open [http://localhost:8000/notebooks](http://localhost:8000/notebooks).
