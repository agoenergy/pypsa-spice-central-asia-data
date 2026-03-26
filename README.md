<!--
-*- coding: utf-8 -*-
SPDX-FileCopyrightText: PyPSA-SPICE Developers
SPDX-License-Identifier: GPL-2.0-or-later
-->

# Dataset for PyPSA-SPICE Central Asia Power System Model

This data repository is used in the PyPSA-SPICE Central Asia model, built on [PyPSA-SPICE](https://agoenergy.github.io/pypsa-spice/), an open-source model builder for evaluating national mid- to long-term energy scenarios through least-cost optimization within the [PyPSA](https://pypsa.org/) framework.

> **Note:** The model covers the **power sector only and does not include district heating**. The results presented in the [publication]() are compatible with PyPSA-SPICE version [v1.1.1](https://agoenergy.github.io/pypsa-spice/releases/#v111-2026-02-24).

If you intend to run the model with this dataset, please follow the steps below to complete the setup.

## 🏗️ Installation

### Step 1: Clone the PyPSA-SPICE repository

Clone the [PyPSA-SPICE repository](https://github.com/agoenergy/pypsa-spice) using **Git**. If you have already cloned the PyPSA-SPICE repository, you can skip this step.

**Important:** The path to the directory where the repository is cloned **must not contain any spaces**.

If Git is not installed on your system, please follow the [Git installation instructions](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git).

```shell title="Cloning the repository"
git clone https://github.com/agoenergy/pypsa-spice.git
cd pypsa-spice
```

> **Note:** For a detailed installation guide for the PyPSA-SPICE model builder, please refer to the [installation guide](https://agoenergy.github.io/pypsa-spice/getting-started/installation/).

### Step 2: Clone this data repository

To clone this data repository into the correct location, navigate into the `data` folder inside the PyPSA-SPICE directory and run the git clone command there.

```shell title="Cloning the pypsa-spice-central-asia-data repository inside the data folder"
cd data
git clone https://github.com/agoenergy/pypsa-spice-central-asia-data.git
cd ..
```

After cloning, the repository will appear inside the `data` folder with its own separate Git version control, independent from PyPSA-SPICE. This ensures that changes to the data repository are tracked separately from the PyPSA-SPICE modelling repository. The resulting folder structure should look as follows:

```text title="Structure of the data repository"
📦 data
 ┗ 📂 global_input_template
 ┗ 📂 scenario_config_template
 ┗ 📂 example
 ┗ 📂 pypsa-spice-central-asia-data
    ┗ 📂 central-asia
      ┗ ...
```

> **Note:** For a detailed description of the input data structure, please refer to [fill in the skeleton CSVs](https://agoenergy.github.io/pypsa-spice/getting-started/input-data/new-model/#step-4-fill-in-the-skeleton-csvs/).

### Step 3: Update base_config.yaml in PyPSA-SPICE

The `base_config_template.yaml` file contains the default configuration for this model. To apply this configuration, copy its contents and replace the existing content in the `base_config.yaml` file located at the root of the PyPSA-SPICE repository.

> **Note:** For a detailed description of the configuration file structure, please refer to the [model builder configuration](https://agoenergy.github.io/pypsa-spice/getting-started/input-data/model-builder-configuration/).

### Step 4: Run the model and explore the output

In `base_config.yaml`, the `input_scenario_name` variable specifies the input scenario folder to use, and `output_scenario_name` specifies the folder where output data will be saved.

Use one of the following commands to run the full workflow. The first example uses 1 process (`-j1`) and 4 threads (`-c4`):

```bash
snakemake -j1 -c4 solve_all_networks
```

Alternatively, to run all rules using all available cores:

```bash
snakemake -call
```

> **Note:** For a detailed description of how to execute the model, please refer to the [model builder execution guide](https://agoenergy.github.io/pypsa-spice/getting-started/input-data/model-builder-execution/).

## Citing PyPSA-SPICE

Please use the citation below:

- Agora Think Tanks (2026): PyPSA-SPICE: PyPSA-based Scenario Planning and Integrated Capacity Expansion

## License

Copyright &copy; [PyPSA-SPICE developers](docs/references/developers.md)

PyPSA-SPICE is licensed under the open source [GNU General Public License v2.0 or later](https://www.gnu.org/licenses/old-licenses/gpl-2.0.en.html)
with the following information:

The documentation is licensed under [CC-BY-4.0](https://interoperable-europe.ec.europa.eu/licence/creative-commons-attribution-40-international-cc-40).
