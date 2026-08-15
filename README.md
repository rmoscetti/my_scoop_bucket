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

| Package | Description |
| --- | --- |
| `open-pdf-studio` | Open-source PDF editor and annotation tool from the OpenAEC Foundation |
| `markitdown` | Command-line tool from Microsoft for converting documents and other files to Markdown, with local vision/OCR support through Ollama |

## Open PDF Studio

[Open PDF Studio](https://github.com/OpenAEC-Foundation/open-pdf-studio) is an open-source PDF editor developed by the OpenAEC Foundation.

It provides PDF annotation and editing features aimed in particular at technical and AEC workflows, including measurements, drawing comparison, redaction, page management and markup tools.

This bucket provides a Scoop manifest for the OpenAEC release of Open PDF Studio.

The package is downloaded from the project's official GitHub releases.

## MarkItDown

[MarkItDown](https://github.com/microsoft/markitdown) is an open-source command-line tool from Microsoft for converting documents and other supported file formats to Markdown.

The Scoop package uses `uv` to create an isolated Python environment and installs MarkItDown with its optional format dependencies and the `markitdown-ocr` plugin.

Two commands are exposed after installation:

```powershell
markitdown
markitdown-ollama
```

### Standard conversion

The standard `markitdown` command uses MarkItDown's native converters:

```powershell
markitdown document.pptx -o document.md
```

This is suitable when the relevant content is available as text or other elements directly handled by the standard converters.

Documents such as PowerPoint presentations can, however, contain significant information inside diagrams, charts, screenshots and other images. The standard conversion may preserve references to these images without extracting the information contained in them.

### OCR and vision support

To improve conversion of visually rich documents, this package also installs Microsoft's `markitdown-ocr` plugin.

The plugin extends MarkItDown with vision-based text extraction for images embedded in PDF, DOCX, PPTX and XLSX files. This is particularly useful for presentations and technical documents where part of the information exists only as graphical content.

For PPTX files, the OCR-enhanced converter can process picture shapes, image placeholders and images contained in groups.

The upstream plugin expects a vision-capable model through an OpenAI-compatible client. This Scoop package adds the `markitdown-ollama` launcher to provide a ready-to-use local configuration based on [Ollama](https://ollama.com/).

The launcher connects to Ollama through its OpenAI-compatible API at:

```text
http://localhost:11434/v1
```

This allows image analysis to run locally, without requiring a commercial cloud API or sending document content to an external service.

The `markitdown-ollama` launcher is specific to this Scoop package and is not part of the upstream MarkItDown project.

### Default vision model

The default model configured for `markitdown-ollama` is:

```text
qwen3-vl:8b
```

[Qwen3-VL](https://ollama.com/library/qwen3-vl) was selected because it is a multimodal model designed to process both text and images, with strong support for OCR, document understanding and visually structured content.

The 8B variant provides a practical balance between recognition quality, model size, memory requirements and inference speed for local document conversion.

Before using the OCR launcher, install the model in Ollama:

```powershell
ollama pull qwen3-vl:8b
```

Then convert a document with:

```powershell
markitdown-ollama presentation.pptx -o presentation.md
```

A different Ollama vision model can be selected with `-m`:

```powershell
markitdown-ollama presentation.pptx -o presentation.md -m <model>
```

The default model can also be overridden through the `MARKITDOWN_OLLAMA_MODEL` environment variable.

### Installing Ollama with Scoop

Ollama is not bundled with the MarkItDown package and is not required when using the standard `markitdown` command.

For a complete Ollama installation including the Windows application and local daemon, use Scoop's `extras` bucket:

```powershell
scoop bucket add extras
scoop install extras/ollama-full
```

Scoop also provides:

```powershell
scoop install main/ollama
```

but the `main/ollama` package contains the command-line component only. When using that package, the Ollama server must be started separately, for example with:

```powershell
ollama serve
```

For use with `markitdown-ollama`, `extras/ollama-full` is therefore the recommended Scoop installation.

Once Ollama is running, download the default vision model:

```powershell
ollama pull qwen3-vl:8b
```

You can verify the installed models with:

```powershell
ollama list
```

Ollama is only required when using:

```powershell
markitdown-ollama
```

The local Ollama server must be running and the selected vision model must already be installed.

## Notes

This repository contains Scoop manifests only.

The packaged software is maintained by its respective upstream projects.

The MarkItDown package installs the upstream `markitdown-ocr` plugin and includes a custom `markitdown-ollama` launcher to integrate it with a local Ollama instance.

The custom launcher defaults to `qwen3-vl:8b`, but any compatible Ollama vision model can be selected explicitly.

This repository is not affiliated with the OpenAEC Foundation, Microsoft, Qwen or Ollama.