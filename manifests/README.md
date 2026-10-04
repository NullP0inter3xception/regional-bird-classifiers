# Training-data manifests

These files preserve the provenance and per-image attribution metadata for the
photos used to build the published regional bird classifiers. The training
images themselves are not included.

| File | Records | Species | Used by |
|---|---:|---:|---|
| [`perth-2026.csv.zip`](perth-2026.csv.zip) | 45,183 | 277 | `perth-v1`, `perth-v1-bioclip25`; unknown-species evaluation for `nl-top350-bioclip25-v1` |
| [`nl-500.csv.zip`](nl-500.csv.zip) | 239,862 | 545 | `nl-top100-v2`, `nl-top350-bioclip25-v1` |

The CSV files are zipped so they remain below GitHub's browser-upload limit.
Each archive contains one CSV file and no macOS metadata files.

## Fields

Both manifests include:

- scientific name;
- relative local filename used during training;
- iNaturalist photo ID;
- Creative Commons licence identifier;
- creator/attribution text; and
- source observation URL.

The Perth manifest additionally contains the English name, direct source URL,
original dimensions, and download timestamp. The Dutch manifest additionally
contains the Dutch name and stored image dimensions.

The local filename is supplied for reproducibility. It is not a substitute for
the creator attribution, source link, and licence when an image is reused.

## Integrity

SHA-256 checksums of the included zip archives:

```text
a42b650818b1527a6697d52c5fb5074facc981e2798fe5dcd4f2c510ae2eb7c8  perth-2026.csv.zip
b15bded94e233383cdc71b8fad3e87e44252e4f3973b3eba2ff928459712a0ab  nl-500.csv.zip
```

SHA-256 checksums after extracting the original CSV files:

```text
27c8c87d074a369143e17c748df007ee0f36f3286b35b4a002bc445ba8fa4e07  perth-2026.csv
9ed7a0087d3972275648c32c8738a5ee83ba1b916b83d6ece9f5bdb843de92c6  nl-500.csv
```

## Licensing notes

The manifests contain only records labelled CC0, CC BY, or CC BY-SA. The
original images retain their individual terms:

- [CC0 1.0](https://creativecommons.org/publicdomain/zero/1.0/)
- [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/)
- [CC BY-SA 4.0](https://creativecommons.org/licenses/by-sa/4.0/)

Always verify the current information on the linked source page before reusing
an image. The current [iNaturalist Terms of Use](https://www.inaturalist.org/pages/terms)
also prohibit using iNaturalist data for commercial AI training.
