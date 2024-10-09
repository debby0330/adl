## How to Train the Model

### Environment  

- **GPU**: NVIDIA GeForce RTX 4060
- **Memory**: 8GB


### 1. Change Directory to Data Folder

Assuming all training data is in the `data` folder, change the path to the `data` folder in the cmd:

```cmd
cd path\to\data 
```
### 2. Train the Paragraph Selection Model
To train the paragraph selection model, run the following command:  

```cmd
python Paragraph_Selection_Train.py --train_file .\data\train.json --validation_file .\data\valid.json --test_file .\data\test.json --output_dir .\data\result\ --model_name_or_path "hfl/chinese-lert-base" 
```
### 3. Train the Span Selection Model
To train the Span selection model, run the following command: 
```cmd
python Span_Selection_Train.py --train_file .\data\Predictions_Paragraph.json --validation_file .\data\valid.json --test_file .\data\test.json --output_dir .\data\result\ --model_name_or_path "hfl/chinese-lert-base" --learning_rete 5e-6 --per_device_train_batch_size 16 --num_train_epochs 200
```



  


   

   
