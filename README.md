<p align="center">
    <img src="https://v1.ax1x.com/2024/04/13/7ySieU.png" width="500" style="margin-bottom: 0.2;"/>
<p>

<h3 align="center"> <a href="https://arxiv.org/abs/2311.06607">Monkey: Image Resolution and Text Label Are Important Things for Large Multi-modal Models</a></h3>
<h2></h2>

<h5 align="center"> Please give us a star ⭐ for the latest update.  </h5>

<h5 align="center">

 
[![arXiv](https://img.shields.io/badge/Arxiv-2311.06607-b31b1b.svg?logo=arXiv)](https://arxiv.org/abs/2311.06607) 
[![License](https://img.shields.io/badge/License-Apache%202.0-yellow)](https://github.com/Yuliang-Liu/Monkey/blob/main/LICENSE) 
[![GitHub issues](https://img.shields.io/github/issues/Yuliang-Liu/Monkey?color=critical&label=Issues)](https://github.com/Yuliang-Liu/Monkey/issues?q=is%3Aopen+is%3Aissue)
[![GitHub closed issues](https://img.shields.io/github/issues-closed/Yuliang-Liu/Monkey?color=success&label=Issues)](https://github.com/Yuliang-Liu/Monkey/issues?q=is%3Aissue+is%3Aclosed)  <br>
</h5>


<details open><summary>💡 Monkey series projects:✨. </summary><p>
<!--  may -->

>[CVPR'24] [**Monkey: Image Resolution and Text Label Are Important Things for Large Multi-modal Models**](https://arxiv.org/abs/2311.06607)<br>
> Zhang Li, Biao Yang, Qiang Liu, Zhiyin Ma, Shuo Zhang, Jingxu Yang, Yabo Sun, Yuliang Liu, Xiang Bai <br>
[![Paper](https://img.shields.io/badge/Paper-CVPR'24_Highlight-red)](README.md)
[![Source_code](https://img.shields.io/badge/Code-Available-white)](README.md)
[![Demo](https://img.shields.io/badge/Demo-blue)](http://vlrlab-monkey.xyz:7681/)
[![Detailed Caption](https://img.shields.io/badge/Detailed_Caption-yellow)](http://huggingface.co/datasets/echo840/Detailed_Caption)
[![Model Weight](https://img.shields.io/badge/Model_Weight-gray)](http://huggingface.co/echo840/Monkey)
[![Model Weight in Wisemodel](https://img.shields.io/badge/Model_Weight_in_Wisemodel-gray)](https://www.wisemodel.cn/models/HUST-VLRLab/Monkey/)
[![Demo in Wisemodel](https://img.shields.io/badge/Demo_in_Wisemodel-blue)](https://wisemodel.cn/space/gradio/huakeMonkey)



> [**TextMonkey: An OCR-Free Large Multimodal Model for Understanding Document**](https://arxiv.org/abs/2403.04473)<br>
> Yuliang Liu, Biao Yang, Qiang Liu, Zhang Li, Zhiyin Ma, Shuo Zhang, Xiang Bai <br>
[![arXiv](https://img.shields.io/badge/Arxiv-2403.04473-b31b1b.svg?logo=arXiv)](https://arxiv.org/abs/2403.04473) 
[![Source_code](https://img.shields.io/badge/Code-Available-white)](monkey_model/text_monkey/README.md)
[![Demo](https://img.shields.io/badge/Demo-blue)](http://vlrlab-monkey.xyz:7684/)
[![Data](https://img.shields.io/badge/Data-yellow)](https://www.modelscope.cn/datasets/lvskiller/TextMonkey_data)
[![Model Weight](https://img.shields.io/badge/Model_Weight-gray)](https://www.modelscope.cn/models/lvskiller/TextMonkey)

    
## News 
* ```2024.4.13 ``` 🚀 Sourced code for [TextMonkey](monkey_model/text_monkey/README.md) is released.
* ```2024.4.5  ``` 🚀 Monkey is nominated as CVPR 2024 Highlight paper.
* ```2024.3.8  ``` 🚀 We release the paper [TextMonkey](https://arxiv.org/abs/2403.04473).
* ```2024.2.27 ``` 🚀 Monkey is accepted by CVPR 2024. 
* ```2024.1.3  ``` 🚀 Release the basic data generation pipeline. [Data Generation](./data_generation)
* ```2023.12.16``` 🚀 Monkey can be trained using 8 NVIDIA 3090 GPUs. See subsection [train](#Train) for details.
* ```2023.11.06``` 🚀 We release the paper [Monkey](https://arxiv.org/abs/2311.06607).

## 🐳 Model Zoo

Monkey-Chat
| Model|Language Model|Transformers(HF) |MMBench-Test|CCBench|MME|SeedBench_IMG|MathVista-MiniTest|HallusionBench-Avg|AI2D Test|OCRBench|
|---------------|---------|-----------------------------------------|---|---|---|---|---|---|---|---|
|Monkey-Chat|Qwev-7B|[🤗echo840/Monkey-Chat](https://huggingface.co/echo840/Monkey-Chat)|72.4|48|1887.4|68.9|34.8|39.3|68.5|534|


## Environment

```python
conda create -n monkey python=3.9
conda activate monkey
git clone https://github.com/Yuliang-Liu/Monkey.git
cd ./Monkey
pip install -r requirements.txt
```


## Train

We also offer Monkey's model definition and training code, which you can explore above. You can execute the training code through executing `finetune_ds_debug.sh`.

The json file used for Monkey training can be downloaded at [Link](https://drive.google.com/file/d/18z_uQTe8Jq61V5rgHtxOt85uKBodbvw1/view?usp=sharing).

**ATTENTION:** Specify the path to your training data, which should be a json file consisting of a list of conversations.

Inspired by Qwen-VL, we freeze the Large Language Model (LLM) and introduce LoRA into four linear layers ```"c_attn", "attn.c_proj", "w1", "w2"``` for training. This step makes it possible to train Monkey using 8 NVIDIA 3090 GPUs. The specific implementation code is in ```modeling_qwen_nvdia3090.py```.

 - Add LoRA: You need to replace the contents of ```modeling_qwen.py``` with the contents of ```modeling_qwen_nvdia3090.py```.
 - Freeze LLM: You need to freeze other modules except LoRA and Resampler modules in ```finetune_multitask.py```.

## Inference
Run the inference code:
```
python ./inference.py --model_path MODEL_PATH  --image_path IMAGE_PATH  --question YOUR_QUESTION
```


## Demo

Demo is fast and easy to use. Simply uploading an image from your desktop or phone, or capture one directly. 
[Demo_chat](http://vlrlab-monkey.xyz:7681) is also launched as an upgraded version of the original demo to deliver an enhanced interactive experience.

We also provide the source code and the model weight for the original demo, allowing you to customize certain parameters for a more unique experience. The specific operations are as follows:
 1. Make sure you have configured the [environment](#environment).
 2. You can choose to use the demo offline or online:
- **Offline:** 
	- Download the [Model Weight](http://huggingface.co/echo840/Monkey). 
	- Modify `DEFAULT_CKPT_PATH="pathto/Monkey"` in the `demo.py` file to your model weight path. 
	- Run the demo using the following command: 
	```
	python demo.py
	```
- **Online:** 
	- Run the demo and download model weights online with the following command: 
	```
	python demo.py -c echo840/Monkey 
	```

Before 14/11/2023, we have observed that for some random pictures Monkey can achieve more accurate results than GPT4V.  
<br>
<p align="center">
    <img src="https://v1.ax1x.com/2024/04/13/7yS2yq.jpg" width="666"/>
<p>
<br>

Before 31/1/2024, Monkey-chat achieved the fifth rank in the Multimodal Model category on [OpenCompass](https://opencompass.org.cn/home). 
<br>
<p align="center">
    <img src="https://v1.ax1x.com/2024/04/13/7yShXL.jpg" width="666"/>
<p>
<br>

 
## Dataset

The json file used for Monkey training can be downloaded at [Link](https://drive.google.com/file/d/18z_uQTe8Jq61V5rgHtxOt85uKBodbvw1/view?usp=sharing).

The data from our multi-level description generation method is now open-sourced and available for download at [Link](https://huggingface.co/datasets/echo840/Detailed_Caption). Examples:

<br>
<p align="center">
    <img src="https://v1.ax1x.com/2024/04/13/7yS6Ss.jpg" width="666"/>
<p>
<br>
	
You can download train images from [Train](https://pan.baidu.com/s/1svSjXTxWpI-3boALgSeLlw). Extraction code: 4hdh

You can download test images and jsonls from [Test](https://pan.baidu.com/s/1ABrQKeE9QBeKvtGzXfM8Eg). Extraction code: 5h71

The images are from CC3M, COCO Caption, TextCaps, VQAV2, OKVQA, GQA, ScienceQA, VizWiz, TextVQA, OCRVQA, ESTVQA, STVQA, AI2D and DUE_Benchmark. When using the data, it is necessary to comply with the protocols of the original dataset.

## Evaluate

We offer evaluation code for 14 Visual Question Answering (VQA) datasets in the `evaluate_vqa.py` file, facilitating a quick verification of results.  The specific operations are as follows:

 1. Make sure you have configured the [environment](#environment).
 2. Modify `sys.path.append("pathto/Monkey")`  to the project path.
 3. Prepare the datasets required for evaluation. 
 4. Run the evaluation code.

 Take ESTVQA as an example:
 - Prepare data according to the following directory structure:
```
├── data
|	├── estvqa
|		├── test_image
|			├── {image_path0}
|			├── {image_path1}
|				  ·
|				  ·
|	├── estvqa.jsonl
```
 - Example of the format of each line of the annotated `.jsonl` file:
```
{"image": "data/estvqa/test_image/011364.jpg", "question": "What is this store?", "answer": "pizzeria", "question_id": 0}
```
 - Modify the dictionary `ds_collections`:
```
ds_collections = {
	'estvqa_test': {
		'test': 'data/estvqa/estvqa.jsonl',
		'metric': 'anls',
		'max_new_tokens': 100,
	},
	...
}
```
 - Run the following command:
```
bash eval/eval.sh 'EVAL_PTH' 'SAVE_NAME'
```


## Citing Monkey
If you wish to refer to the baseline results published here, please use the following BibTeX entries:

```BibTeX
@inproceedings{li2023monkey,
  title={Monkey: Image Resolution and Text Label Are Important Things for Large Multi-modal Models},
  author={Li, Zhang and Yang, Biao and Liu, Qiang and Ma, Zhiyin and Zhang, Shuo and Yang, Jingxu and Sun, Yabo and Liu, Yuliang and Bai, Xiang},
  booktitle={proceedings of the IEEE/CVF conference on computer vision and pattern recognition},
  year={2024}
}
@article{liu2024textmonkey,
  title={TextMonkey: An OCR-Free Large Multimodal Model for Understanding Document},
  author={Liu, Yuliang and Yang, Biao and Liu, Qiang and Li, Zhang and Ma, Zhiyin and Zhang, Shuo and Bai, Xiang},
  journal={arXiv preprint arXiv:2403.04473},
  year={2024}
}
```

## Acknowledgement

[Qwen-VL](https://github.com/QwenLM/Qwen-VL.git), [LLAMA](https://github.com/meta-llama/llama), [LLaVA](https://github.com/haotian-liu/LLaVA), [OpenCompass](https://github.com/open-compass/opencompass), [InternLM](https://github.com/InternLM/InternLM). 


## Copyright
We welcome suggestions to help us improve the Monkey. For any query, please contact Dr. Yuliang Liu: ylliu@hust.edu.cn. If you find something interesting, please also feel free to share with us through email or open an issue. Thanks!
