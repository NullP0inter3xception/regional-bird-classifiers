# Regional bird classifiers

This repository contains interchangeable regional bird classifiers. Each model
is a trained linear classification layer on top of a fixed BioCLIP image
encoder. The training images are not included.

> **Status: MVP.** These classifiers are initial usable versions intended for
> testing and demonstrations. They have not yet been validated broadly enough
> for production use, scientific research, conservation management, or
> decisions involving protected species.

## Selected releases

| Directory | Region | Classes | Encoder | Species-list source |
|---|---|---:|---|---|
| [`perth-v1-bioclip25`](perth-v1-bioclip25/) | Perth and Augusta-Margaret River | 273 | BioCLIP 2.5 Huge | Combined Avibase checklists |
| [`nl-top350-bioclip25-v1`](nl-top350-bioclip25-v1/) | Netherlands | 350 | BioCLIP 2.5 Huge | Dutch candidate list; final selection by unique training observations |
| [`perth-v1`](perth-v1/) | Perth and Augusta-Margaret River | 273 | BioCLIP 2 | Combined Avibase checklists |
| [`nl-top100-v2`](nl-top100-v2/) | Netherlands | 300 | BioCLIP 2 | Observation counts from Waarneming.nl |

`nl-top100-v2` is a historical directory name. Its contents and `model.json`
describe a 300-class model.

Each selected directory contains a `SOURCES.md` file documenting its sources,
training configuration, validation results, and limitations.

## Training-data provenance

The training images were obtained through public iNaturalist observations. The
local manifest records the scientific name, filename, photo ID, creator and
attribution, observation URL, and photo licence for every image. The manifests
used for these models contain only `CC0`, `CC BY`, and `CC BY-SA` images. A
small number of observation links point to iNaturalist network partners such as
NatureWatch New Zealand.

The complete photo manifests are included in [`manifests/`](manifests/). The
training images themselves are not part of this repository, so this publication
does not redistribute third-party photos. Anyone reusing the original images
must comply with the per-image licence and attribution recorded in the manifest
and on the source observation page.

The regional species lists were assembled as follows:

- **Perth:** the [Perth](https://avibase.bsc-eoc.org/checklist.jsp?region=AUwape01)
  and [Augusta-Margaret River](https://avibase.bsc-eoc.org/checklist.jsp?list=howardmoore&region=AUwaam01)
  Avibase checklists were combined. The intended selection was approximately
  the top 270; the published model artefacts contain 273 classes.
- **Netherlands:** the original ranking was based on observation counts from
  [Waarneming.nl](https://waarneming.nl/). For
  `nl-top350-bioclip25-v1`, the final embedded metadata also records
  `dataset_observations`: the 350 classes were ranked within the available
  dataset by the number of unique `observation_url` values. This prevents
  multiple photos from one observation from being counted more than once.

## BioCLIP

- [BioCLIP 2 model card](https://huggingface.co/imageomics/bioclip-2)
- [BioCLIP 2.5 Huge model card](https://huggingface.co/imageomics/bioclip-2.5-vith14)
- [BioCLIP 2 source code and licence](https://github.com/Imageomics/bioclip-2)
- [BioCLIP 2 paper](https://proceedings.neurips.cc/paper_files/paper/2025/hash/94da80cbfe870c1db958c88a8a27018c-Abstract-Conference.html)

BioCLIP 2 produces 768-dimensional embeddings; BioCLIP 2.5 Huge produces
1,024-dimensional embeddings. A classifier can only be used with the encoder
for which it was trained.

## Accuracy

The figures below come from the test split stored in each `classifier.json`.
They are useful as an indication, but do not guarantee performance on new
images or under different field conditions.

These are MVP-level evaluation results. They show that the classifiers are
usable, but do not replace independent field testing across devices, seasons,
life stages, lighting conditions, and locations.

| Classifier | Raw top-1 | Precision when named | Known images named | Unknown images incorrectly named |
|---|---:|---:|---:|---:|
| `perth-v1-bioclip25` | 90.33% | 97.38% | 65.85% | 0.00%* |
| `nl-top350-bioclip25-v1` | 92.50% | 99.32% | 64.26% | 1.10% |
| `perth-v1` | 86.94% | 97.01% | 66.38% | 0.00%* |
| `nl-top100-v2` | 87.46% | 99.00% | 45.48% | 1.81% |

- **Raw top-1:** how often the highest-scoring class was correct before the
  open-set thresholds could reject a prediction.
- **Precision when named:** how often a displayed species name was correct.
- **Known images named:** the share of known test images that was not rejected
  as unknown. High precision is partly achieved by withholding a species name
  when the classifier is uncertain.
- **Unknown images incorrectly named:** the share of images from species not in
  the classifier that nevertheless received a known species name.

\* The Perth open-set test contained only 14 unknown images from two species.
The measured 0.00% is therefore too uncertain to treat as a general error rate.
The Dutch unknown tests were larger: 4,164 images from 211 species for
`nl-top350-bioclip25-v1`, and 2,433 images from 122 species for
`nl-top100-v2`.

The classifiers are deliberately calibrated conservatively: returning “bird
detected” is preferable to displaying a confident but incorrect species name.
This means precision can be high while a substantial proportion of known test
images remains unnamed.

## Files in each classifier

```text
model.json            model ID, display name, and required encoder
classifier.json       weights, thresholds, training metadata, and validation
supported_birds.json  supported species and display names
species.json          text embeddings used for zero-shot fallback
SOURCES.md            provenance and references for this classifier
```

Shared training-data manifests:

```text
manifests/perth-2026.csv.zip  metadata for 45,183 source photos
manifests/nl-500.csv.zip      metadata for 239,862 source photos
manifests/README.md           field descriptions, checksums, and licensing notes
```

Keep each model directory intact; do not combine files from different models.
Applications loading a classifier should verify its model ID and encoder
dimensions.

## Licensing and responsibility

The original classifier artefacts and classifier documentation are licensed
under [CC BY-NC-SA 4.0](../LICENSE.md), subject to the exclusions stated in that
file. This licence permits non-commercial sharing and adaptation with
attribution and ShareAlike requirements.

Attribution is not the same as a licence. The BioCLIP models are governed by
the terms stated on their respective model cards. The original photos retain
their individual Creative Commons terms. The manifests, third-party
attribution text, BioCLIP materials, and source checklists are not relicensed by
the repository licence.

The current [iNaturalist Terms of Use](https://www.inaturalist.org/pages/terms)
prohibit using iNaturalist data for commercial AI training. This is separate
from the Creative Commons licence attached to each individual photo. Do not
Treat the repository licence and these source-platform terms as separate,
simultaneous requirements.

The classifiers are assistive tools and may misidentify a species or reject a
known species. Do not use their output as the sole basis for research,
conservation management, or decisions involving protected species.
