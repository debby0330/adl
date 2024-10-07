# adl

@author: AC512
"""

總共有5支程式碼，  
分別為第一部分段落選擇的 Paragraph_Selection_Train.py 及 Paragraph_Selection_Predict.py  
還有第二部分答案擷取的 Span_Selection_Train.py 及 Span_Selection_Predict.py   
跟最後 end to end 的 End_to_End_Train.py  
  
<h2>Paragraph_Selection_Train.py 說明<h2>    
  
<h3>執行說明<h3>  
   至hugging face選擇模型，並導入
   將model name or path中的defult設至為要用的模型  
   將dataset_file設至為含有train_data,test_data,valid_data,context_data的資料夾

<h3>參數說明<h3>    

這部分的程式碼是參考老師提供的hugging face的程式碼。  
有做更改的部分主要是model name or path、max_length、batch_size、lr_schedual_type參數。  
model 的部分有嘗試過老師限定的幾個模型，目前試出來效果最好的是 hfl/chinese-lert。  
max_length設為老師推薦的512，跑得比較快  
batch_size也是設為老師建議的2。
lr_schedual_type牽涉到learning_rate收斂策略，目前測試下來效果最好的是cosin with restart  

<h3>主程式說明<h3>     

從390行開始，將原有的變數設置為我們train_data的標題question跟paragraph。  
444行處，將example設為所有的訓練資料。frist_sentences = 答案，second_sentences = 問題。而這邊將答案乘以4是因為一個答案會對應到4個文本。  
451行的[0,0,1,0]、[0,0,0,1].... 代表的是答案對應到四個文本中哪一個正確的文本。  
  
<h2>Paragraph_Selection_Predict.py 說明<h2> 
# 段落選擇模型

本專案包含一個用於從多個段落中選擇與問題最相關段落的模型。該模型使用 Hugging Face 的預訓練模型，並針對多選分類進行微調。

## 需求

請確保已安裝以下內容：

- Python 3.x
- PyTorch
- Transformers 庫
- CUDA（可選，如果要在 GPU 上運行模型）

你可以使用以下指令安裝所需套件：

```bash
pip install torch transformers  

data/context.json: 包含所有段落的資料。
data/test.json: 包含測試問題及其候選段落索引。
results_Paragraph: 預訓練模型的目錄，用來儲存微調後的模型。
Predictions_Paragraph.json: 模型預測結果的輸出檔案。
模型運行
準備好資料：

context.json: 包含所有段落的文本資料。
test.json: 包含每個問題及其對應的段落索引。
確保微調模型已存放於 results_Paragraph 目錄中。

運行以下 Python 程式碼來進行段落預測：

bash
複製程式碼
python your_script.py
your_script.py 是你提供的段落選擇模型的腳本，會自動載入段落和問題，並將預測結果儲存到 Predictions_Paragraph.json 中。

程式流程
載入模型與分詞器：從指定的 model_dir 路徑載入 Hugging Face 預訓練模型和分詞器。
載入資料：從 context.json 中載入段落資料，並從 test.json 中載入問題和對應的段落索引。
預處理輸入：為每個問題與對應的段落選項進行分詞與編碼，準備好模型的輸入資料。
進行預測：將問題與段落選項輸入模型，模型會預測出最相關的段落。
保存結果：將每個問題的預測段落索引儲存到 Predictions_Paragraph.json 中。
輸出
預測結果將會被儲存在 Predictions_Paragraph.json 檔案中，格式如下：

json
複製程式碼
[
  {
    "id": "問題的ID",
    "question": "問題的文本",
    "paragraphs": [段落索引列表],
    "relevant": 最相關段落的索引
  }
]
注意事項
若要更改資料或模型路徑，請修改程式碼中的相應路徑變數。
預設使用 GPU，若無 GPU，程式將自動切換為 CPU 運行。  
  
  <h2>Span_Selection_Train.py 說明<h2>   
    這部分的程式碼是參考老師提供的hugging face的程式碼。    
        
        
<h2>Span_Selection_Train.py 說明<h2>    
  
