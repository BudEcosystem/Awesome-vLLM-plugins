# Awesome vLLM Plugins

A curated list of plugins and extensions built on top of [vLLM](https://github.com/vllm-project/vllm) — hardware backends, custom model integrations, and general plugins that extend vLLM without forking the core.

> PRs welcome! See [Contributing](#contributing) for how to add new plugins.


## Hardware / platform plugins

### Officially listed hardware plugins

These plugins live under the vLLM hardware plugin RFC and are listed in the official installation docs.

| Accelerator                     | Package / Name | Repository                                                   | Notes |
| --------------------------------| -------------- | ------------------------------------------------------------ | ----- |
| **Google TPU**                  | `tpu-inference` | https://github.com/vllm-project/tpu-inference               | TPU backend for vLLM; integrates Google Cloud TPUs. |
| **Ascend NPU**                  | `vllm-ascend`  | https://github.com/vllm-project/vllm-ascend                 | Community-maintained Ascend NPU plugin; reference design for hardware plugins. |
| **Intel Gaudi (HPU)**           | (from source)  | https://github.com/vllm-project/vllm-gaudi                  | Gaudi hardware plugin; optimized kernels and integration. |
| **MetaX MACA GPU**              | (from source)  | https://github.com/MetaX-MACA/vLLM-metax                    | MACA GPU backend with custom platform implementation. |
| **Rebellions ATOM / REBEL NPU** | `vllm-rbln`    | https://github.com/rebellions-sw/vllm-rbln                  | Plugin for Rebellions NPUs (ATOM / REBEL). |
| **IBM Spyre AIU**               | `vllm-spyre`   | https://github.com/vllm-project/vllm-spyre                  | vLLM backend for IBM Spyre AIU. |
| **Cambricon MLU**               | `vllm-mlu`     | https://github.com/Cambricon/vllm-mlu                       | Hardware plugin for Cambricon MLU accelerators. |

> **Note:** The table above is intentionally kept aligned with the hardware plugin list in the official vLLM docs. Check the vLLM installation page for the latest status and compatibility notes.

### Additional platform plugins

Plugins that expose additional accelerators or platform backends using `vllm.platform_plugins` (or that act as de‑facto hardware integrations).

#### Intel OpenVINO backend

- **Name:** vLLM OpenVINO backend  
- **Repo:** https://github.com/vllm-project/vllm-openvino  
- **Summary:**  
  OpenVINO backend for vLLM to run LLMs efficiently on Intel CPUs and GPUs. Focuses on AVX2-class CPUs and Intel iGPU/dGPU, with support for features like prefix caching and chunked prefill.

#### Tenstorrent TT plugin

- **Name:** TT vLLM Plugin  
- **Repo:** https://github.com/dmadicTT/tt-vllm-plugin  
- **Summary:**  
  Platform plugin that extracts the Tenstorrent platform implementation from a vLLM fork and packages it as a standalone plugin, enabling vLLM v1 architecture models to run on Tenstorrent hardware.

#### TCU backend demo

- **Name:** vllm-tcu-plugin-demo  
- **Repo:** https://github.com/leoluopy/vllm-tcu-plugin-demo  
- **Summary:**  
  Educational hardware-backend demo plugin (“TCU”) that walks through platform, attention, worker, custom ops, and distributed communicator implementation for vLLM.

#### AWS Neuron / Trainium / Inferentia platform

- **Name:** Optimum Neuron vLLM platform  
- **Repo:** https://github.com/huggingface/optimum-neuron  
- **Docs:** https://huggingface.co/docs/optimum-neuron/guides/vllm_plugin  
- **Summary:**  
  `optimum-neuron` includes a vLLM `platform` plugin that registers an `optimum-neuron` backend for AWS Trainium and Inferentia. Designed to make serving Neuron‑compiled models via vLLM straightforward.


## Model & architecture plugins

Plugins that register **new model architectures** or large out-of-tree projects using `vllm.general_plugins` (or similar).

### Diffusion language models (LLaDA, Dream)

- **Name:** diffuplug – A vLLM Plugin for Diffusion Language Models  
- **Repo:** https://github.com/akkikiki/diffuplug  
- **Summary:**  
  Registers diffusion LMs such as **LLaDA** and **Dream** with vLLM. Implements custom samplers (e.g. `LLaDASampler`) and adapters so diffusion language models can run through vLLM’s engine.

### OpenVLA (Vision-Language-Action) plugin

- **Name:** openvla-vllm  
- **Repo:** https://github.com/GuanxingLu/openvla-vllm  
- **Summary:**  
  vLLM plugin for [OpenVLA](https://openvla.github.io/) that accelerates offline batch inference for vision‑language‑action models, without needing custom compilation.

### MERaLiON‑2 architecture plugin

- **Name:** vllm-plugin-meralion2  
- **Distribution:** PyPI – https://pypi.org/project/vllm-plugin-meralion2/  
- **Summary:**  
  vLLM plugin to register the **MERaLiON‑2‑10B** model architecture. Distributed as a Python package that plugs into vLLM’s plugin system; supports both v0 and v1 engines for specific vLLM versions.

> If you know of other model‑registration plugins (e.g. for custom multimodal architectures), please open a PR and add them here.


## Feature / IO / integration plugins

Plugins that focus on **features**, **scheduling**, **logging**, or **IO processing** rather than new hardware or models. Many of these are small code packages that hook into:

- `vllm.general_plugins` – for patches and model registration.
- `vllm.io_processor_plugins` – for custom request pre/post‑processing.
- `vllm.stat_logger_plugins` – for metrics exporters and custom stats.

Examples you might encounter:

- **Custom scheduling / patch packages**  
  - Blog & reference implementation: “vLLM Custom Patches” style plugins that add features like priority-based scheduling via a general plugin, typically wiring to `VLLM_PLUGINS` or custom env vars (e.g. `VLLM_CUSTOM_PATCHES`).

- **Logging / metrics plugins**  
  - Packages that register stat loggers via `vllm.stat_logger_plugins` to export metrics to systems like Prometheus, custom APM, or internal dashboards.

> Most of these are still emerging and tend to be internal to companies. This section is intentionally left open for community contributions.


## Official docs & specs

- [vLLM Plugin System (design doc)](https://docs.vllm.ai/en/stable/design/plugin_system/)
- [vLLM `vllm.plugins` API reference](https://docs.vllm.ai/en/latest/api/vllm/plugins/)
- [Registering out-of-tree models](https://docs.vllm.ai/en/stable/contributing/model/registration/)
- [Hardware-pluggable RFC & hardware plugins section in vLLM docs](https://docs.vllm.ai/en/latest/getting_started/installation/#hardware-plugins)


## Tutorials, examples & blog posts

### Official resources

- **vLLM Plugin System (official docs)**  
  https://docs.vllm.ai/en/stable/design/plugin_system/

- **vLLM Installation – Hardware Plugins section**  
  https://docs.vllm.ai/en/latest/getting_started/installation/#hardware-plugins

- **vLLM Ascend Plugin docs**  
  https://docs.vllm.ai/projects/ascend/en/latest/

- **vLLM Gaudi Plugin docs**  
  https://docs.vllm.ai/projects/gaudi/en/latest/dev_guide/plugin_system.html

### Community guides

- **How to Build vLLM Plugins (BUD Ecosystem guide)**  
  – Deep dive into plugin lifecycle, plugin groups, and best practices for writing general & platform plugins.  
  https://blog.budecosystem.com/how-to-build-vllm-plugins-a-comprehensive-developer-guide-with-tips-and-best-practices/

- **How to Make Clean, Maintainable Modifications to vLLM Using the Plugin System**  
  – Practical guide showing how to replace forking/monkey‑patching with a general plugin that manages patches (e.g. priority-based scheduling).  
  https://www.xugj520.cn/en/archives/customize-vllm-plugin-system-guide.html

- **Introducing vLLM Hardware Plugin (Ascend + community story)**  
  – Blog from the vLLM project discussing the hardware-pluggable RFC and how Ascend’s plugin became a reference design.  
  https://blog.vllm.ai/2025/05/12/hardware-plugin.html

- **optimum-neuron vLLM plugin docs (AWS Trainium / Inferentia)**  
  – Hugging Face’s guide on their vLLM platform plugin.  
  https://huggingface.co/docs/optimum-neuron/guides/vllm_plugin



## Contributing

Spotted a new plugin, blog post, or tutorial?

1. **Add an entry** under the appropriate section:
   - Include:
     - Name
     - Short one-line description
     - Link (GitHub, docs, PyPI, or HF card)
     - Plugin type (general / platform / IO / stats / etc.)
2. **Sort alphabetically** within each subsection.
3. **Open a PR** with a brief explanation:
   - What does the plugin do?
   - Which plugin group(s) does it register under?
   - Minimum vLLM version (if known).

This repo aims to list **plugins**, not generic vLLM forks or random scripts. As a rule of thumb: if it doesn’t register entry points under a `vllm.*_plugins` group, it probably doesn’t belong here.


