# my_scoop_bucket

A small Scoop bucket for Windows applications that I want to install and keep updated through Scoop.

At the moment, the bucket is focused on [Open PDF Studio](https://github.com/OpenAEC-Foundation/open-pdf-studio).

## Why Open PDF Studio?

Open PDF Studio is an open-source PDF editor developed by the OpenAEC Foundation.

It is especially interesting for technical and AEC workflows because, besides normal PDF annotation and editing, it includes features such as measurements, drawing comparison, redaction, page management and markup tools.

I created this bucket because I could not find another publicly indexed Scoop manifest for the OpenAEC version of Open PDF Studio.

The goal is simply to make it easy to install and update with Scoop.

## Install

Add the bucket:

```powershell
scoop bucket add rmoscetti https://github.com/rmoscetti/my_scoop_bucket
```

Then install Open PDF Studio:

```powershell
scoop install rmoscetti/open-pdf-studio
```

## Update

```powershell
scoop update
scoop update open-pdf-studio
```

The manifest uses Scoop's `checkver` and `autoupdate` support to follow upstream GitHub releases.

## Available packages

| Package           | Description                                                            |
| ----------------- | ---------------------------------------------------------------------- |
| `open-pdf-studio` | Open-source PDF editor and annotation tool from the OpenAEC Foundation |

## Notes

The application is downloaded directly from the official Open PDF Studio GitHub releases.

This repository only contains the Scoop manifest and is not affiliated with the OpenAEC Foundation.
