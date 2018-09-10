[![Abcdspec-compliant](https://img.shields.io/badge/ABCD_Spec-v1.1-green.svg)](https://github.com/soichih/abcd-spec)
[![Run on Brainlife.io](https://img.shields.io/badge/Brainlife-bl.app.1-blue.svg)](https://doi.org/10.25663/bl.app.1)

# app-example-documentation
This is an example of how to write documentation (readme.md and license.md for Apps on brainlife.io)

This service does the X, Y and Z. Executes code X, Y and Z to perform X, Y and Z analysis.

#### Authors
- Franco Pestilli (franpest@indiana.edu)

#### Contributors
- Soichi Hayashi (hayashis@iu.edu)

#### Funding 
[![NSF-BCS-1734853](https://img.shields.io/badge/NSF-BCS_1734853-blue.svg)](https://nsf.gov/awardsearch/showAward?AWD_ID=1734853)

## Running the App 

### On Brainlife.io

You can submit this App online at [https://doi.org/10.25663/bl.app.1](https://doi.org/10.25663/bl.app.1) via the "Execute" tab.

### Running Locally (on your machine)

1. git clone this repo.
2. Inside the cloned directory, create `config.json` with something like the following content with paths to your input files.

```json
{
        "track": "./input/track/track.tck",
	"dwi": "./input/dtiinit/dwi_aligned_trilin_noMEC.nii.gz",
	"bvecs": "./input/dtiinit/dwi_aligned_trilin_noMEC.nii.bvecs",
	"bvals": "./input/dtiinit/dwi_aligned_trilin_noMEC.nii.bvals",
        "life_discretization": 360,
        "num_iterations": 100
}
```

### Sample Datasets

You can download sample datasets from Brainlife using [Brainlife CLI](https://github.com/brain-life/cli).

```
npm install -g brainlife
bl login
mkdir input
bl dataset download 5a0e604116e499548135de87 && mv 5a0e604116e499548135de87 input/track
bl dataset download 5a0dcb1216e499548135dd27 && mv 5a0dcb1216e499548135dd27 input/dtiinit
```


3. Launch the App by executing `main`

```bash
./main
```

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

#### Product.json
The secondary output of this app is `product.json`. This file allows web interfaces, DB and API calls on the results of the processing. 

### Dependencies

This App requires the following libraries when run locally.

  - singularity: https://singularity.lbl.gov/
  - VISTASOFT: https://github.com/vistalab/vistasoft/
  - ENCODE: https://github.com/brain-life/encode
  - MBA: https://github.com/francopestilli/mba
