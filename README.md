# OCT-SRGAN
### Super-Resolution Generative Adversarial Network for Optical Coherence Tomography
This repository contains a notebook-first, reproducible pipeline for retinal OCT binary classification with SRGAN super-resolution support.

## Project Goals

1. Train baseline binary classifier **Model A** using transfer learning at **128x128**.
2. Train **SRGAN** from **32x32** low-resolution inputs to **128x128** outputs.
3. Show scaled image examples directly in notebooks.
4. Use SRGAN-generated images to train **Model B** for **at least 150 epochs**.
5. Use a **70/30 train-test split**.
6. Apply normalization and augmentation and show transformed samples.
7. Compare Model A vs Model B using **Accuracy, F1, and ROC-AUC**.
8. Save model checkpoints every `n` epochs to survive Colab session resets.

All metrics, figures, and comparisons are displayed inline in notebooks. The pipeline does not write result reports to separate `reports/` or `outputs/` folders.

## Label Mapping

- `NORMAL -> 0`
- `DME -> 1`
- `DRUSEN -> 1`

## Dataset Layout

```text
data/
	train/
		NORMAL/
		DME/
		DRUSEN/
	test/
		NORMAL/
		DME/
		DRUSEN/
```

## Repository Structure

```text
OCT-SRGAN/
	notebooks/
		model_a.ipynb
		srgan.ipynb
		model_b.ipynb
		model_comparison.ipynb
	artifacts/
		splits/
			train_split.csv
			test_split.csv
	checkpoints/
		model_a/
			model_a_epoch_XXX.pth
			model_a_final.pth
		srgan/
			generator_epoch_XXX.pth
			discriminator_epoch_XXX.pth
			generator_final.pth
			discriminator_final.pth
		model_b/
			model_b_epoch_XXX.pth
			model_b_final.pth
	resources/
	README.md
	requirements.txt
	LICENSE
```

## Requirement-to-Notebook Mapping

1. Model A transfer learning at 128x128: `notebooks/model_a.ipynb`
2. SRGAN training 32x32 -> 128x128: `notebooks/srgan.ipynb`
3. Scaled image examples: `notebooks/srgan.ipynb`
4. Model B training on SRGAN images (>=150 epochs): `notebooks/model_b.ipynb`
5. 70/30 split: `notebooks/model_a.ipynb` (persisted to `artifacts/splits/`)
6. Normalization/augmentation and transformed sample visualization: `notebooks/model_a.ipynb`, `notebooks/model_b.ipynb`
7. Accuracy, F1, AUC comparison: `notebooks/model_comparison.ipynb`
8. Save checkpoints every `n` epochs: `notebooks/model_a.ipynb`, `notebooks/srgan.ipynb`, `notebooks/model_b.ipynb`

## Reproducible Run (Google Colab)

1. Open Colab with GPU runtime.
2. Clone/upload this repository.
3. Install dependencies:

```python
!pip install -r requirements.txt
```

4. Run notebooks in order:

1. `notebooks/model_a.ipynb`
2. `notebooks/srgan.ipynb`
3. `notebooks/model_b.ipynb`
4. `notebooks/model_comparison.ipynb`

## Notes on Persistence

- Checkpoints are saved every `n` epochs and at final epoch in `checkpoints/`.
- Metrics and plots are shown directly in notebook outputs.
- Split CSVs are saved under `artifacts/splits/` for deterministic cross-notebook reuse.

## Acknowledgements

- The original OCT dataset was collected and published by Srinivasan et al. (2014).
- Used Generative AI tools as aid for documentation, debugging, and structuring of this project, but all code and documentation were reviewed and verified for accuracy and clarity.