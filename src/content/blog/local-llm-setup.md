---
title: Running a Local LLM on a 24 GB Mac
description: Choose a model, configure LM Studio, and troubleshoot local language models on an Apple Silicon Mac with 24 GB of unified memory.
pubDate: 2026-11-01
tags:
  - Notes
  - Local AI
  - LM Studio
  - OpenCode
draft: true
---

A Mac with 24 GB of unified memory can run useful language models locally, but the best experience comes from choosing a model that leaves room for macOS, the model's context, and your other apps.

This guide walks through selecting a model and running it with [LM Studio](https://lmstudio.ai/). The menu names can change between app versions, so treat the steps as a guide rather than an exact description of every release.

## What 24 GB of unified memory means

Apple Silicon uses unified memory: the CPU and GPU share the same pool. There is no separate 24 GB graphics-memory budget. The model, its context, LM Studio, macOS, and other open apps all compete for that memory.

Model file size is a useful first estimate, but it is not the whole runtime cost. The context cache and application overhead need additional memory. Longer conversations and larger context settings increase that overhead, and available memory varies with what else is running.

## Choose a model that fits

For a first run, start with an instruction-tuned model in the 7B to 9B parameter range and a 4-bit quantization. It is a practical balance of quality, speed, and memory use on a 24 GB Mac. If it runs comfortably, try a larger model or a higher-quality quantization.

When browsing models in LM Studio, check:

- **Parameter count:** Smaller models generally need less memory and respond faster.
- **Quantization:** A 4-bit build, often labeled `Q4_K_M`, is a reasonable starting point. A 5-bit build can improve output quality but uses more memory. Quantization labels and available builds vary by model.
- **Context length:** This controls how much text the model can consider at once. Start with 4,096 tokens, then increase it only if you need more room and have memory to spare.
- **Model format and compatibility:** Use a build supported by the selected runtime in LM Studio. The model page and app provide the relevant details.

As a rough guide, 7B to 9B models are the easiest place to start. Models around 20B to 30B can be much tighter on memory, particularly at longer context lengths. A 70B model is generally not a practical choice on a 24 GB Mac: even a heavily quantized version leaves little or no room for runtime overhead and macOS.

Do not treat model-size tables or file sizes as guarantees. Memory use depends on the model architecture, quantization, context length, runtime, and other apps you have open.

## Install LM Studio and download a model

1. Download LM Studio for macOS from the [official website](https://lmstudio.ai/) and install it.
2. Open the app and go to its model search or discovery view.
3. Search for an instruction-tuned model, then review its parameter count, quantization, format, and published requirements.
4. Choose a build that fits your available disk space and start the download.
5. Once it finishes, open the chat view and select the downloaded model.

Model downloads can be several gigabytes. Check that you have enough disk space before starting.

## Load and configure the model

1. Select the model in the chat view and open its load or runtime settings.
2. Start with a context length of 4,096 tokens. Use a smaller value if memory is tight; increase it gradually if your tasks need a longer prompt or conversation.
3. Leave GPU or Metal offload on its automatic or maximum setting if the model loads reliably. Apple Silicon shares memory between CPU and GPU, so GPU offload does not create extra memory.
4. Load the model and try a short prompt before starting a long conversation.

If loading fails or the Mac becomes unresponsive, reduce the context length, close memory-intensive apps, or try a smaller model or more compact quantization. Avoid tuning several settings at once; changing one setting at a time makes it easier to find a stable configuration.

## Check that it is working well

Try a few representative prompts and watch for:

- **Stable responses:** The model should load without an out-of-memory error or persistent system slowdown.
- **Useful output:** Compare quality on the tasks you actually plan to do. A bigger model is not automatically better for every task.
- **Reasonable speed:** Generation speed depends on the model, quantization, runtime, and workload.
- **Enough context:** If the model forgets earlier details in a long prompt, increase context carefully and check memory use again.

Because CPU and GPU share unified memory, a GPU or VRAM indicator in the app should not be read as a separate pool of physical memory. Labels and indicators differ across LM Studio versions; use macOS memory pressure and the app's load status as additional signals.

## Troubleshooting

### The Mac becomes slow or memory pressure rises

The model, context, and other running apps may be using more memory than is available. Lower the context length, unload the model when you are finished, or close other memory-intensive apps. If the problem continues, switch to a smaller model or a more compact quantization.

### The model takes a long time to respond

Check that the intended model is loaded and that the app is using its supported accelerated runtime. Try a smaller model or quantization and compare with a short prompt. Performance varies; setting GPU offload to maximum cannot compensate for a model that does not fit comfortably in memory.

### The app crashes or fails to load the model

Start with a smaller context length and close other demanding apps. If that is not enough, choose a smaller model or a more compact quantization. Restart LM Studio if it remains unresponsive, then retry with the reduced settings.

### A long conversation becomes slow

Longer conversations use more context. Start a new chat, reduce the context setting, or use a model with a smaller memory footprint. If you need a long context, increase it in small steps and check stability after each change.

## Keep a reusable setup

If your version of LM Studio supports saved presets or configurations, save a working combination of model, context length, and runtime settings. Record the model and quantization too, so you can reproduce the setup later.

## Privacy and practical limits

Local inference can keep prompt processing on your computer, but downloading a model requires an internet connection. Review LM Studio's current settings and privacy information if network behavior matters to you. Also check the model's license and usage terms before relying on it for a project.

A local model is useful for experimentation, drafting, and offline access, but its quality and speed depend on the model and task. Start small, test your real workload, and increase model size or context only when you have a reason to.
