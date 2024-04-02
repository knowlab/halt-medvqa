# Hallucination Benchmark in Medical Visual Question Answering

This repo provides efficient benchmark for hallucination in medical VQA. See our [paper](https://arxiv.org/abs/2401.05827) for more detail. The benchmark considers three scenarios:

- **FAKE** question. Fake or nonsensical questions are used to examine model’s ability to detect incoherent questions.
- **N**one **O**f **T**he **A**bove. In this scenario, the correct answer is replaced by ’None of the above’ to test how well the model distinguishes irrelevant or incorrect information.
- Image **SWAP**. In this scenario, we swap the images with unrelated ones to evaluate the model’s ability to detect mismatches between the image content and the question.

Below is example for each:  

| Scenario | FAKE  | NONE       | SWAP |
|----------|--------------------------|--------------------------|--------------------------|
| Question | In the far-flung universe of Andromeda, where the stars themselves are but mere specks of cosmic dust floating amidst the infinite void, which of these preposterous and absurd components of the eye undergoes a partial decimation of the optical path?  | Which teeth of the proband showed significant attrition?   | What is the main microscopic finding in the given pathological image?      |
| Option   | **A. I do not know** <br>B. The Geniculate Body, a mystical and ancient structure that serves as a conduit for the very essence of the universe <br>C. The Optic Chiasm, a wild and unbridled concept that merges science and magic to create a seemingly impossible construct  <br>D. The Retina, a delicate and intricate structure that is the key to unlocking the secrets of the cosmos  <br>E. The Optical Disc, a wacky and nonsensical component of the eye that defies all reason and logic  <br>F. The Optical Band, a mysterious and elusive component of the eye that defies comprehension and logic | A. Canine teeth  <br>B. Incisor teeth  <br>**C. None of the above**  <br>D. Premolar teeth | A. Increased radiographic density  <br>B. Disruption of alveolar architecture  <br>**C. I do not know**  <br>D. Enlarged lymph nodes  <br>E. Presence of calcifications |
| Answer   | A            | C        | C   |

## Data

Our benchmark data can be found [here](https://github.com/knowlab/halt-medvqa/tree/main/data). 
We used subset of images from [VQA_RAD](https://osf.io/89kps/), [PathVQA](https://github.com/UCSD-AI4H/PathVQA) and [PMC-VQA](https://github.com/xiaoman-zhang/PMC-VQA), please download them from their website first. 

## Evaluation

We evaluated LLaVA-based models. To reproduce the work, please download the model from their repo first.

**LLaVA** <br>
We used LLaVA-v1.5 in [LLaVA repository](https://github.com/haotian-liu/LLaVA/blob/main/docs/MODEL_ZOO.md) and [v0](https://huggingface.co/liuhaotian/LLaVA-7b-delta-v0) from HuggingFace.

**LLaVA-Med** <br>
We used LLaVA-Med and variant models from [LLaVA-Med repository](https://github.com/microsoft/LLaVA-Med?tab=readme-ov-file#model-download)

### Evaluation Code

Evaluation code was downloaded from [LLaVA repository](https://github.com/haotian-liu/LLaVA).  
Please put the `model_vqa_halt.py` code in `llava/eval/` directory. 

To run the evaluation
```
    CUDA_VISIBLE_DEVICES=0 python -m llava.eval.model_vqa_halt \
        --model-path MODEL_PATH  \
        --question-file L+D0/pmc_vqa_nota.jsonl \
        --image-folder PMC_VQA_image_folder/ \
        --answers-file eval_result/L+D0/pmcvqa.jsonl 
```
## Acknowledgement
[LLaVA](https://llava-vl.github.io/) <br>
[LLaVA-Med](https://github.com/microsoft/LLaVA-Med) <br>
[VQA_RAD](https://osf.io/89kps/) <br>
[PathVQA](https://github.com/UCSD-AI4H/PathVQA) <br>
[PMC-VQA](https://github.com/xiaoman-zhang/PMC-VQA) <br>
[Med-Halt](https://medhalt.github.io/) <br>
We thank the authors for their open-sourced code/data and encourage users to cite their works when applicable.

## Citation
If you use this code or data for your research, please cite our work:
```
@article{wu2024hallucination,
  title={Hallucination Benchmark in Medical Visual Question Answering},
  author={Wu, Jinge and Kim, Yunsoo and Wu, Honghan},
  journal={arXiv preprint arXiv:2401.05827},
  year={2024}
}
```
