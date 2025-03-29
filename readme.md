# NLP Project <img src="https://github.com/user-attachments/assets/6a8e7f73-1b41-458e-a281-ca76c22e527c" width="50" height="50" />
Pizza Order Parsing System 
- [Overview](#overview)
- [Dataset](#data)
- [Key Features](#feat)
- [Project Pipeline](#pipe)
- [Final Results](#final)
- [Contributors](#contributors)

## <img src="https://github.com/AhmedSamy02/Adders-Mania/assets/88517271/9ed3ee67-0407-4c82-9e29-4faa76d1ac44" width="50" height="50" /> Overview <a name = "overview"></a>
This project develops a Natural Language Processing (NLP) system to interpret complex pizza orders, transforming natural language requests into structured data. The system accurately identifies key components like pizza sizes, toppings (with modifiers), crust types, and drink orders, organizing them into a parse tree structure.

## <img src="https://github.com/user-attachments/assets/347077b8-ead5-4122-a543-1cbb35bb2f85" width="50" height="50" /> Dataset <a name = "data"></a>
Built on the **Amazon Pizza Order Dataset**—a real-world corpus of 2.4M+ orders.  
The dataset comprises a set of annotated commands related to pizza orders, with each entry labeled for entities such as ingredients, pizza types, sizes, and customization
options.  
The dataset portion sizes are as follows:
  1. The training set contains 2,456,446 samples.
  2. The dev set contains 348 samples.


## <img src="https://github.com/user-attachments/assets/97bcb0d9-e3e8-41b1-8bf3-f334b7b2b6af" width="50" height="50" />Key Features <a name = "feat"></a>
- Processes natural language pizza orders with complex requests (e.g., "two large pizzas with extra cheese but no onions")
- Identifies and classifies:
  - Pizza attributes (size, quantity, style)
  - Toppings with modifiers (extra, light, no)
  - Drink orders (type, container, quantity)
- Generates structured parse trees representing order semantics
- Handles negation scopes (e.g., "no peppers or onions")


## <img src="https://github.com/YaraHisham61/Arabic-Font-Recognition/assets/88517271/a1f4f29e-84dd-4a24-871c-8a9118265430" width="30" height="30" /> Project Pipeline <a name = "pipe"></a>
Data Preprocessing
1.	Expanded abbreviations and handled negations.
2.	Removed stop words and duplicates from the training dataset.
________________________________________
Model Architecture
1. Order Classification Model: identifies the boundaries of pizza and drink orders
  -	Data Labeling: 
    -	Used regex to identify and label words in the train.TOP as B-Pizza, I-Pizza, B-Drink, or I-Drink based on their association with pizza or drink orders.
  -	Embeddings: FastText embeddings were used for word representations.
  -	Dataset: Trained on 500K randomly sampled rows from the dataset.
  -	Training: 
    -	Optimizer: Adam
    - Loss: sparse_categorical_crossentropy
    -	Early stopping with the restoration of best weights.
    -	Epochs: 10
  - Model Summary:
    
    | Layer (type)               | Output Shape      | Param #   |
    |----------------------------|-------------------|-----------|
    | InputLayer                 | (None, 45)        | 0         |
    | Embedding                  | (None, 45, 60)    | 18,000    |
    | Bidirectional LSTM         | (None, 45, 256)   | 193,536   |
    | Dense (Output)             | (None, 45, 17)    | 4,369     |
    
     - Total params: 212,821 (831.33 KB)
     - Trainable params: 194,821 (761.02 KB)
     - Non-trainable params: 18,000 (70.31 KB)

2. Entity Recognition Model: identifies key entities within each order to one of the following
```
tags = [
    'O',
    'B-NUMBER', 'I-NUMBER',
    'B-DRINKTYPE', 'I-DRINKTYPE',
    'B-VOLUME', 'I-VOLUME',
    'B-TOPPING', 'I-TOPPING',
    'B-SIZE', 'I-SIZE',
    'B-QUANTITY', 'I-QUANTITY',
    'B-STYLE', 'I-STYLE',
    'B-CONTAINER', 'I-CONTAINER',
    'B-NOT-TOPPING', 'I-NOT-TOPPING',
    'B-NOT-STYLE' , 'I-NOT-STYLE'
]
```
  -	Data Labeling: 
    -	Used regex to map frequently occurring patterns in the train.TOP and train.EXR to entity tags.
  -	Dataset: Trained on 500K randomly sampled rows from the dataset.
  -	Training: 
    -	Optimizer: RMSprop
    -	Loss: sparse_categorical_crossentropy
## <img src="https://github.com/YaraHisham61/Arabic-Font-Recognition/assets/88517271/f42b863b-c284-4db9-bb59-00b9062f0f3d" width="50" height="50" /> Final Results <a name = "final"></a>
Our system achieved 80% exact match accuracy on the development dataset and an average of 73% on the test dataset.

## <img src="https://github.com/YaraHisham61/OS_Scheduler/assets/88517271/859c6d0a-d951-4135-b420-6ca35c403803" width="50" height="50" /> Contributors <a name = "contributors"></a>
<table>
  <tr>
   <td align="center">
    <a href="https://github.com/AhmedSamy02" target="_black">
    <img src="https://avatars.githubusercontent.com/u/96637750?v=4" width="150px;" alt="Ahmed Samy"/>
    <br />
    <sub><b>Ahmed Samy</b></sub></a>
    </td>
   <td align="center">
    <a href="https://github.com/kaokab33" target="_black">
    <img src="https://avatars.githubusercontent.com/u/93781327?v=4" width="150px;" alt="Kareem Samy"/>
    <br />
    <sub><b>Kareem Samy</b></sub></a>
    </td>
   <td align="center">
    <a href="https://github.com/nancyalgazzar" target="_black">
    <img src="https://avatars.githubusercontent.com/u/94644017?v=4" width="150px;" alt="Nancy Ayman"/>
    <br />
    <sub><b>Nancy Ayman</b></sub></a>
    </td>
   <td align="center">
    <a href="https://github.com/YaraHisham61" target="_black">
    <img src="https://avatars.githubusercontent.com/u/88517271?v=4" width="150px;" alt="Yara Hisham"/>
    <br />
    <sub><b>Yara Hisham</b></sub></a>
    </td>
  </tr>
 </table>
