# 🚀 Awesome vLLM Plugins

[![Awesome](https://awesome.re/badge.svg)](https://awesome.re)
[![vLLM](https://img.shields.io/badge/vLLM-Plugin%20Ecosystem-blue?logo=data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHZpZXdCb3g9IjAgMCAyNCAyNCI+PHBhdGggZmlsbD0id2hpdGUiIGQ9Ik0xMiAyTDIgNnY2YzAgNS41NSAzLjg0IDEwLjc0IDkgMTIgNS4xNi0xLjI2IDktNi40NSA5LTEyVjZsLTEwLTR6Ii8+PC9zdmc+)](https://github.com/vllm-project/vllm)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)](https://github.com/your-repo/pulls)
[![License](https://img.shields.io/badge/license-Apache%202.0-blue.svg)](LICENSE)

A curated list of plugins and extensions built on top of [vLLM](https://github.com/vllm-project/vllm) — hardware backends, custom model integrations, and general plugins that extend vLLM without forking the core.

> 🎉 **PRs welcome!** See [Contributing](#-contributing) for how to add new plugins.


## 🔌 Hardware / Platform Plugins

### ✅ Officially Listed Hardware Plugins

These plugins live under the vLLM hardware plugin RFC and are listed in the official installation docs.

| Accelerator | Package / Name | Repository | Notes |
| ----------- | -------------- | ---------- | ----- |
| 🔷 **Ascend NPU** | `vllm-ascend` | [![GitHub](https://img.shields.io/badge/GitHub-repo-black?logo=github)](https://github.com/vllm-project/vllm-ascend) | Community-maintained Ascend NPU plugin; reference design for hardware plugins. |
| 💠 **Intel Gaudi (HPU)** | `(from source)` | [![GitHub](https://img.shields.io/badge/GitHub-repo-black?logo=github)](https://github.com/vllm-project/vllm-gaudi) | Gaudi hardware plugin; optimized kernels and integration. |
| 🔵 **IBM Spyre AIU** | `vllm-spyre` | [![GitHub](https://img.shields.io/badge/GitHub-repo-black?logo=github)](https://github.com/vllm-project/vllm-spyre) | vLLM backend for IBM Spyre AIU. |
| 💠 **Intel OpenVINO** | `(from source)` | [![GitHub](https://img.shields.io/badge/GitHub-repo-black?logo=github)](https://github.com/vllm-project/vllm-openvino) | OpenVINO backend for vLLM to run LLMs efficiently on Intel CPUs and GPUs. Focuses on AVX2-class CPUs and Intel iGPU/dGPU, with support for features like prefix caching and chunked prefill. |

> 📝 **Note:** The table above is intentionally kept aligned with the hardware plugin list in the official vLLM docs. Check the vLLM installation page for the latest status and compatibility notes.

### 🧩 Additional Platform Plugins

Plugins that expose additional accelerators or platform backends using `vllm.platform_plugins` (or that act as de‑facto hardware integrations).

| Platform | Package / Name | Repository | Notes |
| -------- | ---- | ---------- | ----- |
| 🎮 **MetaX MACA GPU** | `(from source)` | [![GitHub](https://img.shields.io/badge/GitHub-repo-black?logo=github)](https://github.com/MetaX-MACA/vLLM-metax) | MACA GPU backend with custom platform implementation. |
| 🔶 **Tenstorrent** | `(from source)` | [![GitHub](https://img.shields.io/badge/GitHub-repo-black?logo=github)](https://github.com/dmadicTT/tt-vllm-plugin) | Platform plugin that extracts the Tenstorrent platform implementation from a vLLM fork and packages it as a standalone plugin, enabling vLLM v1 architecture models to run on Tenstorrent hardware. |
| 🟣 **Cambricon MLU** | `(from source)` | [![GitHub](https://img.shields.io/badge/GitHub-repo-black?logo=github)](https://github.com/Cambricon/vllm-mlu) | Hardware plugin for Cambricon MLU accelerators. |
| ⚡ **Rebellions ATOM / REBEL NPU** | `vllm-rbln` | [![GitHub](https://img.shields.io/badge/GitHub-repo-black?logo=github)](https://github.com/rebellions-sw/vllm-rbln) | Plugin for Rebellions NPUs (ATOM / REBEL). |


## 🧠 Model & Architecture Plugins

Plugins that register **new model architectures** or large out-of-tree projects using `vllm.general_plugins` (or similar).

| Model / Architecture | Name | Repository / Distribution | Notes |
| -------------------- | ---- | ------------------------- | ----- |
| 🌀 **Diffusion LMs (LLaDA, Dream)** | diffuplug | [![GitHub](https://img.shields.io/badge/GitHub-repo-black?logo=github)](https://github.com/akkikiki/diffuplug) | Registers diffusion LMs such as LLaDA and Dream with vLLM. Implements custom samplers (e.g. `LLaDASampler`) and adapters so diffusion language models can run through vLLM's engine. |
| 🤖 **OpenVLA (Vision-Language-Action)** | openvla-vllm | [![GitHub](https://img.shields.io/badge/GitHub-repo-black?logo=github)](https://github.com/GuanxingLu/openvla-vllm) | vLLM plugin for [OpenVLA](https://openvla.github.io/) that accelerates offline batch inference for vision‑language‑action models, without needing custom compilation. |

> 💡 If you know of other model‑registration plugins (e.g. for custom multimodal architectures), please open a PR and add them here!


## 🎯 Decoder Plugins

Plugins that implement custom decoding strategies, sampling methods, and logits processors for advanced text generation.

| Decoder | Name | Repository | Notes |
| ------- | ---- | ---------- | ----- |
| 🧠 **Chain-of-Thought Decoder** | vllm-cot-decoder | [![GitHub](https://img.shields.io/badge/GitHub-repo-black?logo=github)](https://github.com/BudEcosystem/vllm-plugins/tree/main/plugins/vllm-cot-decoder) | Confidence-weighted CoT decoding that adapts sampling based on model certainty. Sharpens predictions when confident, enables exploration when uncertain. ~1.1× overhead. |
| 📊 **Entropy Decoder** | vllm-entropy-decoder | [![GitHub](https://img.shields.io/badge/GitHub-repo-black?logo=github)](https://github.com/BudEcosystem/vllm-plugins/tree/main/plugins/vllm-entropy-decoder) | Adaptive entropy-based decoding using entropy + varentropy metrics. Dynamically adjusts temperature and filtering based on model uncertainty patterns. |

> 🔬 These decoder plugins are part of the [BudEcosystem vLLM Plugins](https://github.com/BudEcosystem/vllm-plugins) collection.


## ⚙️ Feature / IO / Integration Plugins

Plugins that focus on **features**, **scheduling**, **logging**, or **IO processing** rather than new hardware or models. Many of these are small code packages that hook into:

- 🔧 `vllm.general_plugins` – for patches and model registration.
- 📥 `vllm.io_processor_plugins` – for custom request pre/post‑processing.
- 📊 `vllm.stat_logger_plugins` – for metrics exporters and custom stats.

Examples you might encounter:

- 📅 **Custom scheduling / patch packages**
  - Blog & reference implementation: "vLLM Custom Patches" style plugins that add features like priority-based scheduling via a general plugin, typically wiring to `VLLM_PLUGINS` or custom env vars (e.g. `VLLM_CUSTOM_PATCHES`).

- 📈 **Logging / metrics plugins**
  - Packages that register stat loggers via `vllm.stat_logger_plugins` to export metrics to systems like Prometheus, custom APM, or internal dashboards.

> 🚧 Most of these are still emerging and tend to be internal to companies. This section is intentionally left open for community contributions.


## 📚 Official Docs & Specs

- [vLLM Plugin System (design doc)](https://docs.vllm.ai/en/stable/design/plugin_system/)
- [vLLM `vllm.plugins` API reference](https://docs.vllm.ai/en/latest/api/vllm/plugins/)
- [Registering out-of-tree models](https://docs.vllm.ai/en/stable/contributing/model/registration/)
- [Hardware-pluggable RFC & hardware plugins section in vLLM docs](https://docs.vllm.ai/en/latest/getting_started/installation/#hardware-plugins)


## 📖 Tutorials, Examples & Blog Posts

### 🏛️ Official Resources

- **vLLM Plugin System (official docs)**
  https://docs.vllm.ai/en/stable/design/plugin_system/

- **vLLM Installation – Hardware Plugins section**
  https://docs.vllm.ai/en/latest/getting_started/installation/#hardware-plugins

- **vLLM Ascend Plugin docs**
  https://docs.vllm.ai/projects/ascend/en/latest/

- **vLLM Gaudi Plugin docs**
  https://docs.vllm.ai/projects/gaudi/en/latest/dev_guide/plugin_system.html

### 🌍 Community Guides

- **How to Build vLLM Plugins (BUD Ecosystem guide)**
  – Deep dive into plugin lifecycle, plugin groups, and best practices for writing general & platform plugins.
  https://blog.budecosystem.com/how-to-build-vllm-plugins-a-comprehensive-developer-guide-with-tips-and-best-practices/

- **How to Make Clean, Maintainable Modifications to vLLM Using the Plugin System**
  – Practical guide showing how to replace forking/monkey‑patching with a general plugin that manages patches (e.g. priority-based scheduling).
  https://www.xugj520.cn/en/archives/customize-vllm-plugin-system-guide.html

- **Introducing vLLM Hardware Plugin (Ascend + community story)**
  – Blog from the vLLM project discussing the hardware-pluggable RFC and how Ascend's plugin became a reference design.
  https://blog.vllm.ai/2025/05/12/hardware-plugin.html

- **optimum-neuron vLLM plugin docs (AWS Trainium / Inferentia)**
  – Hugging Face's guide on their vLLM platform plugin.
  https://huggingface.co/docs/optimum-neuron/guides/vllm_plugin



## 🤝 Contributing

Spotted a new plugin, blog post, or tutorial?

1. ➕ **Add an entry** under the appropriate section:
   - Include:
     - Name
     - Short one-line description
     - Link (GitHub, docs, PyPI, or HF card)
     - Plugin type (general / platform / IO / stats / etc.)
2. 🔤 **Sort alphabetically** within each subsection.
3. 📬 **Open a PR** with a brief explanation:
   - What does the plugin do?
   - Which plugin group(s) does it register under?
   - Minimum vLLM version (if known).

This repo aims to list **plugins**, not generic vLLM forks or random scripts. As a rule of thumb: if it doesn't register entry points under a `vllm.*_plugins` group, it probably doesn't belong here.

---

<p align="center">
  ⭐ Star this repo if you find it useful! ⭐
</p>


