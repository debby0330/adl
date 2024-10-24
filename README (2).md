# HW 2

## Environment

- **GPU**: NVIDIA GeForce RTX 4060
- **Memory**: 8GB


```shell
# build a conda environment called "py3810"
make
conda activate py3810
pip install -r requirements.txt
```



### 1. Change Directory to Data Folder

Assuming training program call news_summarize_train.py and the testing program call predict_mT5.py, are in the `adl` folder. And all the training data is in the `data` folder which is under `adl` folder, change the path to the `adl` folder in the cmd:

```cmd
cd path\to\adl
```

### 2. Train the news summarize model
To train the model, run the following command:  

```cmd
python news_summarize_train.py --model_name_or_path yihsuan/mt5_chinese_small --train_file .\data\separate_train8.json --validation_file .\data\separate_validation2.json --per_device_train_batch_size 16 --gradient_accumulation_steps 4 --max_source_length 256 --max_target_length 64 --learning_rate 3e-5 --num_warmup_steps 680 --num_train_epochs 10 --output_dir .\models\mt5-small_chinese_E10_warmup_3e5_B64_ML256 
```

### 2. Test the news summarize model
To test the model, run the following command:  

```cmd
python predict_mT5.py --model_name_or_path .\models\mt5-small_chinese_E10_warmup_3e5_B64_ML256 --output_dir .\data\public_submission_.jsonl --num_beams 5 --test_file .\data\public.jsonl
```


