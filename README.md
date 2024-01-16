# halt-medvqa

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

