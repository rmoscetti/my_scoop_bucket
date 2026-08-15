# my_scoop_bucket

Personal Scoop bucket for Windows software and command-line tools that I want to install and keep updated through Scoop.

## Install

Add the bucket:

```
scoop bucket add rmoscetti https://github.com/rmoscetti/my_scoop_bucket
```

Then install a package:

```
scoop install rmoscetti/open-pdf-studioscoop install rmoscetti/markitdown
```

## Update

Update Scoop and the installed packages:

```
scoop updatescoop update open-pdf-studioscoop update markitdown
```

The manifests use Scoop's `checkver` and `autoupdate` support where appropriate to track upstream releases.

## Available packages

| Package           | Description                                                                                                                                  |
| ----------------- | -------------------------------------------------------------------------------------------------------------------------------------------- |
| `open-pdf-studio` | Open-source PDF editor and annotation tool from the OpenAEC Foundation                                                                       |
| `markitdown`      | Command-line tool from Microsoft for converting documents and other files to Markdown, with optional local vision/OCR support through Ollama |

## Open PDF Studio

[Open PDF Studio](https://github.com/OpenAEC-Foundation/open-pdf-studio) is an open-source PDF editor developed by the OpenAEC Foundation.

It provides PDF annotation and editing features aimed in particular at technical and AEC workflows, including measurements, drawing comparison, redaction, page management and markup tools.

This bucket provides a Scoop manifest for the OpenAEC release of Open PDF Studio.

The package is downloaded from the project's official GitHub releases.

## MarkItDown

[MarkItDown](https://github.com/microsoft/markitdown) is an open-source command-line tool from Microsoft for converting documents and other supported file formats to Markdown.

The Scoop package uses `uv` to create an isolated Python environment and installs MarkItDown together with its optional format dependencies.

Two commands are exposed after installation:

```
markitdownmarkitdown-ollama
```

### Standard conversion

The standard `markitdown` command uses MarkItDown's native converters:

```
markitdown document.pptx -o document.md
```

This works well for extracting text and document structure.

For PowerPoint files, however, images may only appear in the generated Markdown as references such as `Picture1.jpg`, without being exported or interpreted. This can result in significant information loss when slides rely heavily on diagrams, charts, screenshots or other visual content.

### OCR and vision support

To improve conversion of visually rich documents, the package also installs the `markitdown-ocr` plugin.

The plugin allows images contained in supported documents to be processed by a vision-capable language model. This is particularly useful for PowerPoint presentations where relevant information may be contained in diagrams, charts, screenshots or other graphical elements rather than as native text.

The OCR functionality is exposed through the additional `markitdown-ollama` launcher included in this package.

It is configured to use a local [Ollama](https://ollama.com/) server through its OpenAI-compatible API:

```
http://localhost:11434/v1
```

This allows vision processing to run locally without requiring a commercial cloud API or sending document content to an external service.

### Default vision model

The default model is:

```
qwen3-vl:8b
```

[Qwen3-VL](https://ollama.com/library/qwen3-vl) was selected because it is designed for multimodal image and text processing and performs well on OCR, document understanding and visually structured content.

The 8B variant provides a practical balance between recognition quality, memory requirements and inference speed for local document conversion.

The model must be installed in Ollama before using the OCR launcher:

```
ollama pull qwen3-vl:8b
```

Then convert a document with:

```
markitdown-ollama presentation.pptx -o presentation.md
```

A different Ollama vision model can be selected with `-m`:

```
markitdown-ollama presentation.pptx -o presentation.md -m <model>
```

The default model can also be overridden through the `MARKITDOWN_OLLAMA_MODEL` environment variable.

### Installing Ollama

Ollama is not bundled with the MarkItDown package and is not required for standard conversions.

Ollama is available through Scoop's official `main` bucket, which is enabled by default:

```
scoop install ollama
```

The explicit bucket-qualified form is also valid:

```
scoop install main/ollama
```

Once Ollama is installed, download the default vision model used by `markitdown-ollama`:

```
ollama pull qwen3-vl:8b
```

Ollama is only required when using:

```
markitdown-ollama
```

The Ollama service must be running locally and the selected vision model must already be installed.

## Notes

This repository contains Scoop manifests only.

The packaged software is maintained by its respective upstream projects.

The MarkItDown package includes a small custom launcher for integrating `markitdown-ocr` with a local Ollama instance. The launcher is specific to this Scoop package and is not part of the upstream MarkItDown project.

This repository is not affiliated with the OpenAEC Foundation, Microsoft, Alibaba/Qwen or Ollama.
