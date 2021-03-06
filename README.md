# ![MultiQC](https://raw.githubusercontent.com/ewels/MultiQC/master/docs/images/MultiQC_logo.png)

# Montage
## MultiQC for Chemical GlycoBiology
### Aggregate chemical glycobiology results across many samples into a single report.

This fork includes computational chemistry, glycoinformatics and chemical biology tools.


[![Documentation Status](https://readthedocs.org/projects/montage/badge/?version=latest)](https://montage.readthedocs.io/en/latest/?badge=latest)
[![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.1068992.svg)](https://doi.org/10.5281/zenodo.1068992)


-Find MultiQC [documentation](http://multiqc.info/docs) and [example reports](http://multiqc.info/examples/rna-seq/multiqc_report.html) at [http://multiqc.info](http://multiqc.info)



Montage is written in Python (tested with v 3.6). 

Currently, supported computational, glycoinformatics and chemical biology tools include:

|Molecular Dynamics               | Quantum Chemistry      | Post-dynamics analysis (e.g. Ring Pucker) | Other |
|---------------------------------|------------------------|---------------------------|----------------------|
|                                 |comp_qm                 |montage_tessellate             |                      |


## Installation

### Prerequisite dev environment
Install Ananconda python3, then create an environment for MultiQC

```
conda create -n multiqc python=3
source activate multiqc
```

### clone the code

```
git clone git@github.com:scientificomputing/Montage.git
# OR git clone https://github.com/scientificomputing/Montage.git
pushd Montage
```

### compile the code
```
make install

```
If make fails, look for required dependencies and install them, for example:

```
sudo yum install libyaml-devel libpng-devel -y
make install
```

## Usage

### Tessellate example

[Install the tessellate tool](https://github.com/scientificomputing/tessellate)

The tessellate part:
```
source activate multiqc
pip install tessellate
wget https://github.com/scientificomputing/tessellate/tree/master/data
tessellate data/usecase-timeseries --input-format=builtin --output-format=json --output-dir=output-usecase-timeseries
```

The Montage part:
```
export DATAPATH=`pwd`
multiqc $DATAPATH/output-usecase-timeseries -m montage_tessellate 
multiqc $DATAPATH/output-usecase-rnadna -m montage_tessellate 
multiqc $DATAPATH/output-usecase-cyclodextrin -m montage_tessellate 

```

### QM example
Select log files from the data dir, only use the quantum analysis module and force creation of a report (overwrites existing):

```bash
multiqc data/*.log -m comp_qm -f
```

### General usage
Once installed, you can use MultiQC by navigating to your analysis directory
(or a parent directory) and running the tool:
```bash
multiqc .
```


## Development

### New modules
Create a new module, e.g. add module newmodule in multiqcc say multiqc/modules/newmodule/*
A great example to work from is kallisto

Then include newmodule in:
 - multiqc/utils/search_patterns.yaml
 - setup.py


# Future ideas (which may be fixed by core multiqc or highcharts dev)

- render windows separately for large report. i.e. turn pieces on and off for memory intensive report
- fix colour scales to include negative numbers
- include all modules within the montage module, so usage will be -m montage and all submodule will be run
- pip install that does not clash with multiqc. Ideally without renaming the main codebase. 
  - If changes to the main code base become very exotic (some are in the pipeline), then this fork will diverge heavily from the base of multiqc and will need be renamed. Otherwise Montage will be a plugin for multiqc, a pull request will be submitted.

# Credits
[This package is a fork of MultiQC](https://github.com/ewels/MultiQC/)
[Project Lead & Contributors for MultiQC](README-multiqc.md)
Montage credits [@chrisbarnetttser](https://github.com/chrisbarnettster)



