[![Abcdspec-compliant](https://img.shields.io/badge/ABCD_Spec-v1.0-green.svg)](https://github.com/soichih/abcd-spec)

# app-example-documentation
This is an example of how to write documentation (readme.md and license.md for Apps on brainlife.io)

This service does the X, Y and Z. Executes code X, Y and Z to perform X, Y and Z analysis.

## Running the App 

### Using Docker

First, create output directory and store your config.json contaning path to your input files (relative to /input that you are going to specify below)

```bash
cat > config.json << CONF
{
        "t1": "/input/sub-FP/anatomy/t1.nii.gz",
        "track": "/input/sub-FP/tractography/run01_fliprot_aligned_trilin_csd_lmax10_wm_SD_PROB-NUM01-500000.tck",
	"dwi": "/input/sub-FP/dwi/run01_fliprot_aligned_trilin.nii.gz",
	"bvecs": "/input/sub-FP/dwi/run01_fliprot_aligned_trilin.bvecs",
	"bvals": "/input/sub-FP/dwi/run01_fliprot_aligned_trilin.bvals",
        "life_discretization": 360,
        "num_iterations": 100
}
CONF
```

Then, launch brainlife/life

```bash
docker run --rm -it \
	-v /mnt/v1/testdata:/input \
	-v `pwd`:/output \
	brainlife/life
```

* Replace `/mnt/v1/testdata` to where you have your input files. 
* Replace `pwd` to point to your output directory (if you don't want them to go to your current working directory). If you change this, be sure to move your config.json there also. This container starts up with current directory set to /output.

### Using the Command Line

Note. Currently, this service can only be launched on command line on Resource XYZ.

First, create your config.json

```bash
cat > config.json << CONF
{
        "t1": "/input/sub-FP/anatomy/t1.nii.gz",
        "track": "/input/sub-FP/tractography/run01_fliprot_aligned_trilin_csd_lmax10_wm_SD_PROB-NUM01-500000.tck",
	"dwi": "/input/sub-FP/dwi/run01_fliprot_aligned_trilin.nii.gz",
	"bvecs": "/input/sub-FP/dwi/run01_fliprot_aligned_trilin.bvecs",
	"bvals": "/input/sub-FP/dwi/run01_fliprot_aligned_trilin.bvals",
        "life_discretization": 360,
        "num_iterations": 100
}
CONF
```

Then, execute `start.sh` which will submit a job to PBS queue.

## Output

The main output of this App is a file called `output.mat`. This file contains following object.

```
fe = 

    name: 'temp'
    type: 'faseval'
    life: [1x1 struct]
      fg: [1x1 struct]
     roi: [1x1 struct]
    path: [1x1 struct]
     rep: []
```

`output_fg.pdb` contains all fasicles with >0 weights withtin fg object (fibers)

> TODO.. explain this a bit more..


# Dependencies
This App requires the following libraries when run as shell (not using the compiled docker container).

  VISTASOFT
  ENCODE
  MBA
