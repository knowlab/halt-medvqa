# Hallucination Benchmark in Medical Visual Question Answering

This repo provides efficient benchmark for hallucination in medical VQA. See our [paper](https://arxiv.org/abs/2401.05827) for more detail. The benchmark considers three scenarios:

- **FAKE** question. Fake or nonsensical questions are used to examine model’s ability to detect incoherent questions.
- **N**one **O**f **T**he **A**bove. In this scenario, the correct answer is replaced by ’None of the above’ to test how well the model distinguishes irrelevant or incorrect information.
- Image **SWAP**. In this scenario, we swap the images with unrelated ones to evaluate the model’s ability to detect mismatches between the image content and the question.

Below is example for each:  

| Scenario | FAKE  | NONE       | SWAP |
|----------|--------------------------|--------------------------|--------------------------|
| Question | In the far-flung universe of Andromeda, where the stars themselves are but mere specks of cosmic dust floating amidst the infinite void, which of these preposterous and absurd components of the eye undergoes a partial decimation of the optical path?  | Which teeth of the proband showed significant attrition?   | What is the main microscopic finding in the given pathological image?      |
| Option   | **A. I do not know**  B. The Geniculate Body, a mystical and ancient structure that serves as a conduit for the very essence of the universe  C. The Optic Chiasm, a wild and unbridled concept that merges science and magic to create a seemingly impossible construct  D. The Retina, a delicate and intricate structure that is the key to unlocking the secrets of the cosmos  E. The Optical Disc, a wacky and nonsensical component of the eye that defies all reason and logic  F. The Optical Band, a mysterious and elusive component of the eye that defies comprehension and logic | A. Canine teeth  B. Incisor teeth  **C. None of the above**  D. Premolar teeth | A. Increased radiographic density  B. Disruption of alveolar architecture  **C. I do not know**  D. Enlarged lymph nodes  E. Presence of calcifications |
| Answer   | A            | C        | C   |



## Model Download

### LLaVA
We used LLaVA-v1.5 in [LLaVA repository](https://github.com/haotian-liu/LLaVA/blob/main/docs/MODEL_ZOO.md) and [v0](https://huggingface.co/liuhaotian/LLaVA-7b-delta-v0) from HuggingFace.

### LLaVA-Med
We used LLaVA-Med and variant models from [LLaVA-Med repository](https://github.com/microsoft/LLaVA-Med?tab=readme-ov-file#model-download)

## Evaluation Code

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

