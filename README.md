# PCOS Cluster Prediction

A Python Jupyter Notebook for batch submission of clinical, anthropometric, hormonal and metabolic data to the PcosX PCOS subtype prediction web tool.

## Overview

This notebook provides a simple workflow for submitting multiple observations to the web endpoint used by the PcosX prediction tool.

PcosX was developed by Gao et al. and collaborators as part of their research into data-driven subtypes of polycystic ovary syndrome (PCOS).

The original PcosX web tool is available at:

www.pcos.org.cn

This repository does not implement, reproduce or modify the underlying PcosX prediction model. It automates the submission of input data to the web service and retrieves the returned cluster prediction for each observation.

## What the notebook does

For each row in an input Excel file, the notebook:

1. Reads the required input variables.
2. Converts missing values to blank strings and formats values for submission.
3. Constructs the request payload expected by the PcosX web endpoint.
4. Submits the data to the endpoint.
5. Retrieves the predicted cluster and associated response information.
6. Appends the returned results to the original dataset.
7. Saves the combined data to a new Excel file.


## Input data

The notebook expects an Excel file named:

`dataset.xlsx`

Users should provide their own appropriately formatted dataset.

The following columns are expected:

| Column | Variable |
|---|---|
| `height` | Height |
| `weight` | Weight |
| `BMI` | Body mass index |
| `lh` | Luteinising hormone |
| `fsh` | Follicle-stimulating hormone |
| `testosterone` | Testosterone |
| `shbg` | Sex hormone-binding globulin |
| `amh` | Anti-Müllerian hormone |
| `dheas` | Dehydroepiandrosterone sulfate |
| `fasting_blood_glucose` | Fasting blood glucose |
| `fasting_insulin` | Fasting insulin |
| `hdl` | High-density lipoprotein cholesterol |

Column names should match those listed above.

## Output

The results are saved as:

`pcos_predictions.xlsx`

The output file contains the original input data together with the following additional columns:

| Column | Description |
|---|---|
| `api_code` | Response code returned by the web service |
| `api_msg` | Response message returned by the web service |
| `predicted_cluster` | Predicted PCOS cluster |
| `api_id` | ID returned by the web service |

If a request fails, the error is recorded in `api_msg` and the corresponding prediction fields are left empty.

## Requirements

The notebook requires Python 3 and the following packages:

```bash
pip install pandas requests openpyxl
```

The Python `time` module is also used but is part of the standard library and does not require separate installation.

## Usage

1. Download or clone this repository.
2. Place your input Excel file in the same working directory as the notebook.
3. Name the input file:

   `dataset.xlsx`

4. Open:

   `pcos_cluster_prediction.ipynb`

5. Run the notebook cells sequentially.

6. The completed results will be saved as:

   `pcos_predictions.xlsx`

## Data privacy

No participant-level research data are included in this repository.

Users should not commit or upload sensitive, confidential or identifiable datasets to a public repository.

The notebook submits selected input variables to an external web service. Users are responsible for ensuring that any data submitted to the service are appropriate for transmission and that their use complies with applicable ethical approvals, institutional policies, data-governance requirements and legislation.


## Acknowledgement and citation

The underlying PCOS subtype classification approach and PcosX web tool were developed by Gao et al. and collaborators.

If using this workflow in research, please acknowledge and cite the original work:

**Gao X, Zhao S, Du Y, et al. Data-driven subtypes of polycystic ovary syndrome and their association with clinical outcomes. Nature Medicine. 2025;31:4214–4224.**

DOI: `10.1038/s41591-025-03984-1`

PcosX web tool: `www.pcos.org.cn`

Please refer to the original publication for details of the development, validation and interpretation of the PCOS subtype classification model.

## Disclaimer

This repository is an independent utility and is not affiliated with, endorsed by or maintained by the developers of PcosX.

The underlying PCOS subtype classification model and PcosX web tool are the work of their original authors and institutions. This repository does not contain or reproduce the underlying prediction model.

The code simply automates submission of appropriately formatted data to the web endpoint used by PcosX and records the returned results.

The availability of the PcosX website should not be interpreted as permission for unrestricted automated or high-volume access. Users intending to use this workflow at scale, for publication or as part of a formal research study should confirm that their intended use is consistent with the terms and expectations of the PcosX developers.
