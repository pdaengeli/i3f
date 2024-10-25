# IIIF Presentation Manifests

IIIF presentation manifests play a key role in the DSE-AS projects in two fields:

* import of images into Transkribus
* contextual presentation of images on the web

Given that the image resources are distributed over a number of archives and libraries, IIIF manifests are created to handle the information in a uniform way.

## Principle 

This repository contains an automated workflow that generates IIIF presentation manifests for documents.

The generation is based on a short declaration containing the image links.

When *pushing* a commit containing one or more `.toml` files to the `main` branch of this repository, manifests are generated and made available automatically.

## Specifics

The document declaration uses a minimal language called [TOML](https://en.wikipedia.org/wiki/TOML).

The files are conventionally saved in the `input` directory and named following the pattern `{type}_nnnnn`, e.g. `shortform_00001` or `letter_00001`. 

The concordance of documents and document identifiers is defined elsewhere.

## TOML template

```
mf_id = "{type}_nnnnn.json"
mf_lang = "en"
mf_label = "{some title/label of document}"

# IIIF image links as a sequence of key/value pairs under `[mf_data]`

[mf_data]
"{mf_id}_nnn" = "https://{iiif-server}/{path}/{identifier}/info.json"
```
Note that double quotes are not allowed within values (use single quotes instead).

## Development

`ipynb` outputs may be accessed under `debug` (`debug/generate-manifests.html`, `debug/generate-manifests.ipynb`).

Manifests may be tested using

* https://presentation-validator.iiif.io/
* https://presentation-validator.iiif.io/validate?version=3.0&url= + manifest URL [programmatically]
* https://uv-v4.netlify.app/#?manifest= + manifest URL [visually]
* or other viewers (Mirador is known to be fickly at times)