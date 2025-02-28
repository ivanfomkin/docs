---

__system: {"dislikeVariants":["No answer to my question","Recomendations didn't help","The content doesn't match title","Other"]}
---
# Platforms

{{ compute-full-name }} provides various types of physical processors. Choosing a platform guarantees the type of physical processor in the data center and determines the set of valid vCPU and RAM configurations. You can also add a graphics accelerator (GPU) to a VM. You must choose a platform when creating each VM.

## Standard platforms {#standard-platforms}

| Platform | Processor | Maximum number of cores</br>(vCPUs) per VM | CPU base</br>clock rate (GHz) |
| --- | --- | --- | --- |
| Intel Broadwell</br>(`standard-v1`) | [Intel® Xeon® Processor E5-2660 v4](https://ark.intel.com/content/www/us/en/ark/products/91772/intel-xeon-processor-e5-2660-v4-35m-cache-2-00-ghz.html) | 32 | 2.00 |
| Intel Cascade Lake</br>(`standard-v2`) | [Intel Xeon Gold 6230](https://ark.intel.com/content/www/us/en/ark/products/192437/intel-xeon-gold-6230-processor-27-5m-cache-2-10-ghz.html) | 80 | 2.10 |

## Platforms with GPUs {#gpu-platforms}

| Platform | Graphics</br>accelerator | Processor | Characteristics |
| --- | --- | --- | --- |
| Intel Broadwell with</br>NVIDIA® Tesla® V100</br>(`gpu-standard-v1`) | [NVIDIA® Tesla® V100](https://www.nvidia.com/en-us/data-center/v100/) | [Intel Xeon</br>Processor E5-2660 v4](https://ark.intel.com/content/www/us/en/ark/products/91772/intel-xeon-processor-e5-2660-v4-35m-cache-2-00-ghz.html) | **Maximum number of GPUs per VM**: 4 </br> **Number of vCPUs per GPU**: 8 </br> **RAM per GPU**: 96 GB |
| Intel Cascade Lake</br>with NVIDIA® Tesla® V100</br>(`gpu-standard-v2`) | [NVIDIA® Tesla® V100](https://www.nvidia.com/en-us/data-center/v100/) | [Intel Xeon Gold 6230](https://www.intel.com/content/www/us/en/products/processors/xeon/scalable/gold-processors/gold-6230.html) | **Maximum number of GPUs per VM**: 8 </br> **Number of vCPUs per GPU**: 8 </br> **RAM per GPU**: 48 GB |

## Platforms with vGPUs {#vgpu-platforms}

| Platform | Graphics</br>accelerator | Processor | Characteristics |
| --- | --- | --- | --- |
| Intel Broadwell with</br>NVIDIA® vGPU Tesla® V100 8G</br>(`vgpu-standard-v1`) | [NVIDIA® Tesla® V100](https://www.nvidia.com/en-us/data-center/v100/) | [Intel Xeon</br>Processor E5-2660 v4](https://ark.intel.com/content/www/us/en/ark/products/91772/intel-xeon-processor-e5-2660-v4-35m-cache-2-00-ghz.html) | **Number of vGPUs**: 1</br>**Number of vCPUs**: 4</br>**RAM**: 12 GB</br>**GPU RAM**: 8 GB |

## See also {#see-also}

* [Permissible vCPU and RAM configurations](performance-levels.md).
* [Permitted GPU, vCPU, and RAM configurations](gpus.md#config).
* [Pricing for computing resources on different platforms](../pricing.md#prices).

