<!--
-*- coding: utf-8 -*-
SPDX-FileCopyrightText: PyPSA-SPICE Developers
SPDX-License-Identifier: CC-BY-4.0
-->

# Dataset for Cross-Border Power System Integration Analysis in Central Asia Using PyPSA-SPICE

This data repository is used in the [Cross-Border Power System Integration Analysis](https://www.agora-energiewende.org/publications/cross-border-power-system-integration-in-central-asia) study, built on [PyPSA-SPICE](https://agoenergy.github.io/pypsa-spice/), an open-source model builder for evaluating national mid- to long-term energy scenarios through least-cost optimization within the [PyPSA](https://pypsa.org/) framework.

> **Note:** The model covers the **power sector only and does not include district heating**. The results presented in the [study]([https://www.agora-energiewende.org/publications](https://www.agora-energiewende.org/publications/cross-border-power-system-integration-in-central-asia)) are compatible with PyPSA-SPICE version [v1.1.1](https://agoenergy.github.io/pypsa-spice/releases/#v111-2026-02-24) with hourly resolution.

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
      ┗ 📂 input
      ┗ 📂 results
      ┗ ...
```

> **Note:** For a detailed description of the input data structure, please refer to [fill in the skeleton CSVs](https://agoenergy.github.io/pypsa-spice/getting-started/input-data/new-model/#step-4-fill-in-the-skeleton-csvs/).

### Step 3: Update base_config.yaml in PyPSA-SPICE

The `base_config_template.yaml` file contains the default configuration for this model. To apply this configuration, copy its contents and replace the existing content in the `base_config.yaml` file located at the root of the PyPSA-SPICE repository.

> **Note:** For a detailed description of the configuration file structure, please refer to the [model builder configuration](https://agoenergy.github.io/pypsa-spice/getting-started/input-data/model-builder-configuration/).

### Step 4: Run the model

In `base_config.yaml`, the `input_scenario_name` variable specifies the input scenario folder to use, and `output_scenario_name` specifies the folder where output data will be saved.

> **Note:** The results presented in the [publication](https://www.agora-energiewende.org/publications) were generated with hourly resolution using the Gurobi solver. You can also download the published output CSV files from this [link](https://cloud.sefep.eu/s/CNMGSkJ6HkNjfSL), place them directly in the `results` folder, and can proceed with [Step 5](#step-5-explore-the-output-and-visualisation).

> By default, this repository is configured for open-source solvers such as HiGHs and uses a 25-hour step size. To reproduce the publication setup, open `scenario_config.yaml` in each input scenario folder, change `stepsize: 25` to `stepsize: 1` in the `scenario_configs` section, and update the `solver` section from `name: highs` and `options: highs-default` to `name: gurobi` and `options: gurobi-default`. Please note that it might take longer execution time to run with hourly resolution using open-source solvers.

Use one the following commands to run the full workflow. The first example uses 1 process (`-j1`) and 4 threads (`-c4`):

```bash
snakemake -j1 -c4 solve_all_networks
```

Alternatively, to run all rules using all available cores:

```bash
snakemake -call
```

> **Note:** For a detailed description of how to execute the model, please refer to the [model builder execution guide](https://agoenergy.github.io/pypsa-spice/getting-started/input-data/model-builder-execution/).

### Step 5: Explore the output and visualisation

You can run streamlit app with the following command to see the dynamic charts in your web browser (local-host).

```bash
streamlit run pypsa-spice-vis/main.py
```

After running, you will be able to see a local web link/url in the terminal. Simply open the link/url in your browser and you will be able to see the visualisations.

> **Note:** For a detailed description of the output file structure and pypsa-spice-vis tool, please refer to the [PyPSA-SPICE-VIS](https://agoenergy.github.io/pypsa-spice/visualisation-tool/pypsa-spice-vis/).

## Citing this dataset

Please use the citation below:

- Agora Energiewende and University of Central Asia (2026): Cross-border power system integration in Central Asia. Insights from the PyPSA-SPICE Central Asia model.

## License

Copyright &copy; [PyPSA-SPICE developers](docs/references/developers.md)

PyPSA-SPICE is licensed under the open source [GNU General Public License v2.0 or later](https://www.gnu.org/licenses/old-licenses/gpl-2.0.en.html)
with the following information:

The documentation is licensed under [CC-BY-4.0](https://interoperable-europe.ec.europa.eu/licence/creative-commons-attribution-40-international-cc-40).
