# Sources — `perth-v1-bioclip25`

## Model

- Region: Perth and Augusta-Margaret River, Western Australia
- Classes: 273
- Encoder: [BioCLIP 2.5 Huge](https://huggingface.co/imageomics/bioclip-2.5-vith14), ViT-H/14, 1,024-dimensional embeddings
- Pinned revision: `6e3d04e3d6522012c88181085c5ae666e14c45cd`
- OpenCLIP version: 3.3.0
- Maturity: MVP; intended for testing and demonstrations

Exact weights, thresholds, training parameters, and metrics are recorded in
[`classifier.json`](classifier.json). Compatibility metadata is stored in
[`model.json`](model.json).

## Species list

The species list combines the Avibase checklists for
[Perth](https://avibase.bsc-eoc.org/checklist.jsp?region=AUwape01) and
[Augusta-Margaret River](https://avibase.bsc-eoc.org/checklist.jsp?list=howardmoore&region=AUwaam01).
The intended selection was approximately the top 270; the published model
contains 273 classes.

## Training images

Dataset ID: `perth-2026`. The local manifest contains 45,183 photo records
covering 277 species: 32,098 CC BY, 8,800 CC0, and 4,285 CC BY-SA records.
Of the observation links, 45,116 point to iNaturalist and 67 to NatureWatch New
Zealand. Each record preserves the creator and attribution, photo ID,
observation URL, source URL, and licence. The images are not redistributed; the
complete metadata manifest is included as
[`../manifests/perth-2026.csv.zip`](../manifests/perth-2026.csv.zip).

Training used at most 500 known images per species with random seed 42.

## Validation and limitations

Stored test results report 90.33% raw top-1 accuracy and 97.38% precision among
named predictions. The open-set test contained only 14 unknown images from two
species, so its measured 0% false acceptance rate is not a robust real-world
estimate. This MVP classifier has not undergone broad independent field
validation.

## References and terms

- [iNaturalist](https://www.inaturalist.org/)
- [iNaturalist Terms of Use](https://www.inaturalist.org/pages/terms)
- [CC0 1.0](https://creativecommons.org/publicdomain/zero/1.0/)
- [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/)
- [CC BY-SA 4.0](https://creativecommons.org/licenses/by-sa/4.0/)
- [BioCLIP 2.5 Huge model card](https://huggingface.co/imageomics/bioclip-2.5-vith14)
- [BioCLIP 2 paper](https://proceedings.neurips.cc/paper_files/paper/2025/hash/94da80cbfe870c1db958c88a8a27018c-Abstract-Conference.html)

The original images retain their individual licences. Consult the source page
and recorded attribution before reusing an image. The current iNaturalist Terms
of Use also prohibit using iNaturalist data for commercial AI training.
