# my_scoop_bucket

Personal Scoop bucket for Windows software and command-line tools that I want to install and keep updated through Scoop.

## Install

Add the bucket:

```powershell
scoop bucket add rmoscetti https://github.com/rmoscetti/my_scoop_bucket
```

Then install a package:

```powershell
scoop install rmoscetti/open-pdf-studio
scoop install rmoscetti/markitdown
```

## Update

Update Scoop and the installed packages:

```powershell
scoop update
scoop update open-pdf-studio
scoop update markitdown
```

The manifests use Scoop's `checkver` and `autoupdate` support where appropriate to track upstream releases.

## Available packages

| Package           | Description                                                                           |
| ----------------- | ------------------------------------------------------------------------------------- |
| `open-pdf-studio` | Open-source PDF editor and annotation tool from the OpenAEC Foundation                |
| `markitdown`      | Command-line tool from Microsoft for converting documents and other files to Markdown |

## Open PDF Studio

[Open PDF Studio](https://github.com/OpenAEC-Foundation/open-pdf-studio) is an open-source PDF editor developed by the OpenAEC Foundation.

It provides PDF annotation and editing features aimed in particular at technical and AEC workflows, including measurements, drawing comparison, redaction, page management and markup tools.

This bucket provides a Scoop manifest for the OpenAEC release of Open PDF Studio.

The package is downloaded from the project's official GitHub releases.

## MarkItDown

[MarkItDown](https://github.com/microsoft/markitdown) is an open-source command-line tool for converting documents and other supported file formats to Markdown.

The Scoop manifest uses `uv` to create an isolated Python environment and install MarkItDown together with its optional conversion dependencies.

The `markitdown` command is exposed through Scoop after installation.

## Notes

This repository contains Scoop manifests only.

The packaged software is maintained by its respective upstream projects.

This repository is not affiliated with the OpenAEC Foundation or Microsoft.
