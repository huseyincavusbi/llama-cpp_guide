# Model Conversion and Quantization Guide

This guide outlines the steps to convert a Hugging Face `safetensors` model to the `GGUF` format and then quantize it using `llama.cpp`.

## Prerequisites

Before you begin, ensure you have:

-   `llama.cpp` repository cloned and built. If not, follow these steps:

    ```bash
    git clone https://github.com/ggerganov/llama.cpp
    cd llama.cpp
    make
    ```

-   The Hugging Face model you wish to convert (e.g., `LiquidAI/LFM2-700M`) cloned locally.

    ```bash
    git clone https://huggingface.co/LiquidAI/LFM2-700M
    ```

## Steps

### 1. Convert `safetensors` to `GGUF` (F16)

Navigate to your `llama.cpp` directory and use the `convert-hf-to-gguf.py` script to convert your model to the `GGUF` format with `F16` precision. Replace `/Users/hc/Documents/mlx conv/LFM2-700M` with the path to your cloned model.

```bash
python3 llama.cpp/convert_hf_to_gguf.py LFM2-700M --outtype f16 --outfile LFM2-700M-f16.gguf
```

### 2. Quantize the `GGUF` Model

Once you have the `F16` `GGUF` model, you can quantize it to a smaller, more efficient format like `Q4_K_M` using the `llama-quantize` tool. Ensure you are in the `llama.cpp` directory or provide the full path to the `llama-quantize` executable.

```bash
./llama.cpp/build/bin/llama-quantize LFM2-700M-f16.gguf LFM2-700M-q4_k_m.gguf Q4_K_M
```

This will create a new `GGUF` file (`LFM2-700M-q4_k_m.gguf`) with the specified quantization level.


