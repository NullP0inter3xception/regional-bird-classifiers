# Sources — `nl-top350-bioclip25-v1`

## Model

- Region: Netherlands
- Classes: 350
- Encoder: [BioCLIP 2.5 Huge](https://huggingface.co/imageomics/bioclip-2.5-vith14), ViT-H/14, 1,024-dimensional embeddings
- Pinned revision: `6e3d04e3d6522012c88181085c5ae666e14c45cd`
- OpenCLIP version: 3.3.0
- Maturity: MVP; intended for testing and demonstrations

Exact weights, thresholds, training parameters, and metrics are recorded in
[`classifier.json`](classifier.json). Compatibility metadata is stored in
[`model.json`](model.json).

## Species list

The Dutch candidate list was based on observation counts from
[Waarneming.nl](https://waarneming.nl/). For this build, the embedded metadata
then records `rank_by: dataset_observations`: the final 350 classes were ranked
within the available training dataset by the number of unique observation URLs.
This model is therefore not solely a direct snapshot of the Waarneming.nl
ranking.

## Training images

Dataset ID: `nl-500`. The local manifest contains 239,862 photo records
covering 545 species: 195,030 CC BY, 29,766 CC0, and 15,066 CC BY-SA records.
Each record preserves the scientific and Dutch names, creator and attribution,
photo ID, observation URL, and licence. Most links point to iNaturalist; a small
number point to iNaturalist network partners. The images are not redistributed;
the complete metadata manifest is included as
[`../manifests/nl-500.csv.zip`](../manifests/nl-500.csv.zip).

Training used at most 250 known images per species with random seed 42. The
open-set test used Perth species absent from the Dutch training classes.

## Validation and limitations

Stored test results report 92.50% raw top-1 accuracy and 99.32% precision among
named predictions. Of 4,164 unknown test images, 1.10% were incorrectly given a
known species name. This MVP classifier has not undergone broad independent
field validation.

## References and terms

- [Waarneming.nl](https://waarneming.nl/)
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
