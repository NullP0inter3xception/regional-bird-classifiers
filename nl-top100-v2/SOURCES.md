# Sources — `nl-top100-v2`

## Model

- Region: Netherlands
- Classes: 300
- Encoder: [BioCLIP 2](https://huggingface.co/imageomics/bioclip-2), ViT-L/14, 768-dimensional embeddings
- Maturity: MVP; intended for testing and demonstrations

The directory name is historical: `model.json`, the species list, and the
classifier contain 300 classes and identify this model as **Netherlands - Top
300**. This older export does not record an exact BioCLIP revision or OpenCLIP
version.

## Species list

The top 300 was ranked by observation counts from
[Waarneming.nl](https://waarneming.nl/). In `classifier.json`, `observations`
stores the count used for each class and `rank` stores its selection position.

## Training images

The supplied provenance links this model to the Dutch dataset now identified as
`nl-500`; its older metadata still names `vb_bird_dataset500`. The current local
manifest contains 239,862 photo records covering 545 species: 195,030 CC BY,
29,766 CC0, and 15,066 CC BY-SA records. The images are not redistributed; the
complete metadata manifest is included as
[`../manifests/nl-500.csv.zip`](../manifests/nl-500.csv.zip).

Training used at most 500 known images per species with random seed 42.

## Validation and limitations

Stored test results report 87.46% raw top-1 accuracy and 99.00% precision among
named predictions. Of 2,433 unknown test images, 1.81% were incorrectly given a
known species name. This MVP classifier has not undergone broad independent
field validation and is less precisely reproducible than the newer BioCLIP 2.5
classifiers.

## References and terms

- [Waarneming.nl](https://waarneming.nl/)
- [iNaturalist](https://www.inaturalist.org/)
- [iNaturalist Terms of Use](https://www.inaturalist.org/pages/terms)
- [CC0 1.0](https://creativecommons.org/publicdomain/zero/1.0/)
- [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/)
- [CC BY-SA 4.0](https://creativecommons.org/licenses/by-sa/4.0/)
- [BioCLIP 2 model card](https://huggingface.co/imageomics/bioclip-2)
- [BioCLIP 2 source code and licence](https://github.com/Imageomics/bioclip-2)
- [BioCLIP 2 paper](https://proceedings.neurips.cc/paper_files/paper/2025/hash/94da80cbfe870c1db958c88a8a27018c-Abstract-Conference.html)

The original images retain their individual licences. Consult the source page
and recorded attribution before reusing an image. The current iNaturalist Terms
of Use also prohibit using iNaturalist data for commercial AI training.
