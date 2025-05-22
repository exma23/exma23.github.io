---
layout: post
title: Glossary: NLP
subtitle:
categories: glossary
author: tangha1004
tags: [nlp]
---


# W5: Word embedding

1; → các cách chuyển từ NLP sang chuỗi số

2; 1 từ có nghĩa khác 1 token (có thể k có nghĩa); có thể hiểu đơn nghĩa hoặc đa nghĩa

3; trước khi biểu diễn wordembedding → người ta từng dùng wordnet, tập hợp các từ đồng nghĩa lại với nhau → quan hệ “is-a” tạo thành 1 network → cung cấp thông tin về nghĩa của từ và nghĩa của từ bao hàm

4; VD: ô tô và xe đạp cùng là phương tiện đường bộ → có thể chia nhỏ “phương tiện đường bộ” ra thành các nhóm nhỏ khác nhau

Ví dụ nếu sử dụng wordnet có 2 vấn đề

- vấn đề 1: chia chủ đề lớn thành quá nhiều chủ đề nhỏ → khó quản lý; chủ đề quá ít → nghĩa quá rộng hoặc mất nghĩa của từng từ
    - VD: nói về phương tiện di chuyển như ô tô, xe đạp thì đôi khi một số trường hợp cần nghĩa sâu hơn  như nhóm “phương tiện di chuyển” đã chia
    - nếu chỉ dùng wordnet thì không biểu diễn được sự khác nhau giữa 2 từ
    - hoặc wordnet vẫn có thể distinguish giữa 2 từ nhưng chưa biết được là đưa thông tin đó vào máy như nào
- vấn đề 2: word net cố định mà nghĩa của từ có thể thay đổi → ví dụ google trước là tên riêng, giờ gần đồng nghĩa với với search
- vấn đề 3: không thể tính toán → chỉ xét đại diện về mặt nghĩa

5; Đoán nghĩa 1 từ → dựa vào các từ xung quanh 

- Biến từ đó thành 1 vecto embedding → qua model/thuật toán → vecto dạng mới

6; Các dạng vecto

- One hot encoding: hạn chế cực kì về nghĩa và giới hạn số lượng từ
    - sự khác nhau về nghĩa của các từ không rõ rệt → chỉ khác nhau về vị trí của từ mà thôi (present N không khác gì present V)
    - số từ lớn → biểu diễn bằng one-hot encoding k hiệu quả
    
    → nên xem xét cả context của từ nữa
    
- words which frequently appear in similiar contexts have similar meaning
    - VD: bank trong context: cổ phiếu, sổ tiết kiệm → sẽ có cùng nghĩa với bank trong context: i need money
    - a word $w$ appears in a text, its context is the set of words that appear nearby (within a fixed-size window) ⇒ use many contexts to build up a representation of $w$
- distributed representation:
    - vector representation that encodes information about the distribution of contexts a word appears in
- cosine similarity:
    - chuyển biểu diễn nghĩa của từ sang dạng hình học → những từ trái nghĩa với nhau thì có vecto đối chiều nhau
    - ví dụ: x,y biểu diễn bởi vecto $F$  chiều
- TF-IDF: tf-idf(t, d) = tf(t, d) * idf(t)
    - TF: term frequency → giống document term
    - IDF: từ đấy có mối quan hệ như nào với văn bản
    
    ![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/c6ea46c5-8480-4f92-9aa2-5f7a90ec1326/9c6cea04-ab20-42fd-ab7d-61f21944910c/image.png)
    
    - Ma trận TF-IDF sẽ có cùng kích thước với ma trận term document → từng cột sẽ là vecto biểu diễn của cả văn bản đó
    - Tùy từng trường hợp ta có thể sử dụng hàng hoặc cột
- word vectors
    - one hot encoding → mỗi chiều đều có thông tin
    - từng chiều sẽ không cung cấp thông tin cụ thể → cả vector mới là cái meaning
    - word vector là một bản nâng cấp của distributed representation → vẫn biểu diễn từ đó thôi
    - với dạng này → phải tăng cường thông tin context vào trong từ
    - word embedding mong muốn có thông tin về các từ xung quanh → có nhiều hướng để embedding
        - backpropagation
        - neural network
        - word2vec
    - chuyển từ dạng word → không gian
        - kỳ vọng là những từ giống nhau sẽ ở gần nhau trong không gian
        - thể hiện được mối quan hệ giữa các từ ngoài mối quan hệ giữa từ với văn bản
        - Relationships between words correspond to difference between vectors.
            
            ![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/c6ea46c5-8480-4f92-9aa2-5f7a90ec1326/7d99553b-20b5-44fb-9148-2f487cac0cbc/image.png)
            

7; vấn đề khi xây dựng word embedding

- không gian nên có bao chiều
- xây dựng ma trận W trong không gian đó như nào (V hàng n cột)

8; Word2Vec

- Assumption: có một tập văn bản trước → trượt cửa sổ theo từng câu; với mỗi thời điểm ta sẽ xét từ ở chính giữa và các từ xung quanh nó
    - từ từ chính giữa đó → compute probabilities of context words
    - adjust the vectors to increase these probabilities.
- Cần tối ưu hóa thông tin của w_t khi biết thông tin các từ phía trước → theo 2 cách: skipgram và c-bold
    
    ![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/c6ea46c5-8480-4f92-9aa2-5f7a90ec1326/7cfb24b9-2b7e-49f8-bf73-493825cf4ff5/image.png)
    

→ xác suất cần tối ưu hóa là: 

![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/c6ea46c5-8480-4f92-9aa2-5f7a90ec1326/9b7fd657-8e77-4b16-92cd-46d5a9f989c1/image.png)

9; Word2Vec cố gắng dự đoán các từ context dựa vào từ chính giữa 

- For each word we will have two vectors:
v_w when it is a central word;
u_w when it is a context word
- 

![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/c6ea46c5-8480-4f92-9aa2-5f7a90ec1326/8aa5c3f3-7825-4833-a9f5-49dccf0c9b44/image.png)

10; Word2Vec: là 1 neural network để đi tối ưu hóa 1 xác suất

- 2 hướng: CBOW hoặc skipgram
- Objective function: tối ưu hóa là xác suất p(o | c)
- training:

11; Word2Vec → cổ

Glove → 2014

FastText → Facebook 2016

Người ta sử dụng chung language model để convert từ sang embedding luôn

<!-- Lorem ipsum dolor sit amet, consectetur adipiscing elit. Fusce bibendum neque eget nunc mattis eu sollicitudin enim tincidunt. Vestibulum lacus tortor, ultricies id dignissim ac, bibendum in velit.

## Some great heading (h2)

Proin convallis mi ac felis pharetra aliquam. Curabitur dignissim accumsan rutrum. In arcu magna, aliquet vel pretium et, molestie et arcu.

Mauris lobortis nulla et felis ullamcorper bibendum. Phasellus et hendrerit mauris. Proin eget nibh a massa vestibulum pretium. Suspendisse eu nisl a ante aliquet bibendum quis a nunc. Praesent varius interdum vehicula. Aenean risus libero, placerat at vestibulum eget, ultricies eu enim. Praesent nulla tortor, malesuada adipiscing adipiscing sollicitudin, adipiscing eget est.

## Another great heading (h2)

Lorem ipsum dolor sit amet, consectetur adipiscing elit. Fusce bibendum neque eget nunc mattis eu sollicitudin enim tincidunt. Vestibulum lacus tortor, ultricies id dignissim ac, bibendum in velit.

### Some great subheading (h3)

Proin convallis mi ac felis pharetra aliquam. Curabitur dignissim accumsan rutrum. In arcu magna, aliquet vel pretium et, molestie et arcu. Mauris lobortis nulla et felis ullamcorper bibendum.

Phasellus et hendrerit mauris. Proin eget nibh a massa vestibulum pretium. Suspendisse eu nisl a ante aliquet bibendum quis a nunc.

### Some great subheading (h3)

Praesent varius interdum vehicula. Aenean risus libero, placerat at vestibulum eget, ultricies eu enim. Praesent nulla tortor, malesuada adipiscing adipiscing sollicitudin, adipiscing eget est.

> This quote will change your life. It will reveal the secrets of the universe, and all the wonders of humanity. Don't misuse it.

Lorem ipsum dolor sit amet, consectetur adipiscing elit. Fusce bibendum neque eget nunc mattis eu sollicitudin enim tincidunt.

### Some great subheading (h3)

Vestibulum lacus tortor, ultricies id dignissim ac, bibendum in velit. Proin convallis mi ac felis pharetra aliquam. Curabitur dignissim accumsan rutrum.

```html
<html>
  <head> </head>
  <body>
    <p>Hello, World!</p>
  </body>
</html>
```

In arcu magna, aliquet vel pretium et, molestie et arcu. Mauris lobortis nulla et felis ullamcorper bibendum. Phasellus et hendrerit mauris.

#### You might want a sub-subheading (h4)

In arcu magna, aliquet vel pretium et, molestie et arcu. Mauris lobortis nulla et felis ullamcorper bibendum. Phasellus et hendrerit mauris.

In arcu magna, aliquet vel pretium et, molestie et arcu. Mauris lobortis nulla et felis ullamcorper bibendum. Phasellus et hendrerit mauris.

#### But it's probably overkill (h4)

In arcu magna, aliquet vel pretium et, molestie et arcu. Mauris lobortis nulla et felis ullamcorper bibendum. Phasellus et hendrerit mauris.

### Oh hai, an unordered list!!

In arcu magna, aliquet vel pretium et, molestie et arcu. Mauris lobortis nulla et felis ullamcorper bibendum. Phasellus et hendrerit mauris.

- First item, yo
- Second item, dawg
- Third item, what what?!
- Fourth item, fo sheezy my neezy

### Oh hai, an ordered list!!

In arcu magna, aliquet vel pretium et, molestie et arcu. Mauris lobortis nulla et felis ullamcorper bibendum. Phasellus et hendrerit mauris.

1. First item, yo
2. Second item, dawg
3. Third item, what what?!
4. Fourth item, fo sheezy my neezy

## Headings are cool! (h2)

Proin eget nibh a massa vestibulum pretium. Suspendisse eu nisl a ante aliquet bibendum quis a nunc. Praesent varius interdum vehicula. Aenean risus libero, placerat at vestibulum eget, ultricies eu enim. Praesent nulla tortor, malesuada adipiscing adipiscing sollicitudin, adipiscing eget est.

Praesent nulla tortor, malesuada adipiscing adipiscing sollicitudin, adipiscing eget est.

Proin eget nibh a massa vestibulum pretium. Suspendisse eu nisl a ante aliquet bibendum quis a nunc.

### Tables

| Title 1               | Title 2               | Title 3               | Title 4               |
| --------------------- | --------------------- | --------------------- | --------------------- |
| lorem                 | lorem ipsum           | lorem ipsum dolor     | lorem ipsum dolor sit |
| lorem ipsum dolor sit | lorem ipsum dolor sit | lorem ipsum dolor sit | lorem ipsum dolor sit |
| lorem ipsum dolor sit | lorem ipsum dolor sit | lorem ipsum dolor sit | lorem ipsum dolor sit |
| lorem ipsum dolor sit | lorem ipsum dolor sit | lorem ipsum dolor sit | lorem ipsum dolor sit |

| Title 1                    | Title 2                                | Title 3                    | Title 4                                |
| -------------------------- | -------------------------------------- | -------------------------- | -------------------------------------- |
| lorem                      | lorem ipsum                            | lorem ipsum dolor          | lorem ipsum dolor sit                  |
| lorem ipsum dolor sit amet | lorem ipsum dolor sit amet consectetur | lorem ipsum dolor sit amet | lorem ipsum dolor sit                  |
| lorem ipsum dolor          | lorem ipsum                            | lorem                      | lorem ipsum                            |
| lorem ipsum dolor          | lorem ipsum dolor sit                  | lorem ipsum dolor sit amet | lorem ipsum dolor sit amet consectetur | -->


Những gì phải học:

- Transformer
    - Paper: Attention is all you need
    - Explain for 5 years old level:  https://www.youtube.com/watch?v=PSs6nxngL6k&t=836s (1 year ago)
    - Explain step by step: https://www.youtube.com/watch?v=4Bdc55j80l8
    - Minh họa các bước nhân ma trận: https://jalammar.github.io/illustrated-transformer/
    - Thêm toán về attention mechanism: sách Understand Deep learning → muốn đọc thì bảo t gửi
    - Code: https://github.com/jadore801120/attention-is-all-you-need-pytorch
    - Matrix multiplication visualization:
        - even enough for documentation: https://e2eml.school/transformers.html#multihead
        - https://pytorch.org/blog/inside-the-matrix/
        - https://ketanhdoshi.github.io/Transformers-Why/
        - https://forums.fast.ai/t/fun-matrix-math-example-the-transformers-attention-mechanism/41606/5
- BERT:
    - Paper: bidirectional … gốc → của Google (t thấy đọc xong Transformer cũng dễ đọc)
    - Giải thích sơ qua: tra mì AI BERT
    - Minh họa: (tuy t thấy đọc không vào đầu lắm) https://jalammar.github.io/illustrated-bert/
    - Code: https://github.com/google-research/bert
    - Matrix multiplication visualization:
        - https://www.youtube.com/watch?v=90mGPxR2GgY
- Code mình sử dụng
    - Stanford: https://github.com/lry00127/miniBert
    - Dataset: CFIMDB - SST - Quora
        - miniBERT này phát triển từ BTL của CMU: https://github.com/neubig/minbert-assignment → cùng dataset CFIMDB và SST
        
        ![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/c6ea46c5-8480-4f92-9aa2-5f7a90ec1326/aee0beeb-7bf8-4ebe-bbc4-528d1712aef9/image.png)
        

# A; Transformer

## I; Src tự học

- 3b1b: https://www.youtube.com/watch?v=eMlx5fFNoYc (5 months ago)
- step by step explaination: https://www.youtube.com/watch?v=4Bdc55j80l8 (4 years ago)
- Statquest:
    - Attention mechanism intuitive: https://www.youtube.com/watch?v=PSs6nxngL6k&t=836s (1 year ago)
    - Transformer for 5 yo: https://www.youtube.com/watch?v=zxQyTK8quyY (1 year ago)
- Mathematical and implementations:
    - Another youtube series: https://www.youtube.com/watch?v=UPtG_38Oq8o

## II; Original paper

- “Attention is all you need”

## III; Own interpretation of Transformer

(after aggregating information from many sources with code)

### 1; Context of invention

- Old architectures for translating task/general NLP tasks: RNN, LTSM, etc have some disadvantages:
    - Each token is passed seq2seq → make the training process long
    - Can’t make training process parallel with each training example
    - Vanishing/exploding gradients → as seq2seq model with many layers
- Attention → new way of letting other words effect on the embedding of each word
    - without regard to their distance in the input or output sequences

### 2; Architecture overview

![pic1.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/c6ea46c5-8480-4f92-9aa2-5f7a90ec1326/d0dc3645-5fa0-4341-ae89-c7340c5d997b/pic1.png)

- Like sequence models: encoder and decoder part
- Encoder:
    - Input: symbol representation $(x_1,...,x_n)$ - an embedding
        - A sentence: “I am Ha” → $x_1$  is NOT a embedding vector  of “I” (sometimes SOS  - start of sentence symbol) constructed by the vocabulary/ dictionary in the dataset
        - There are many other types of embedding. 1 hot encoding from the vocabulary is just one type
        - Depends on the type of embedding → $d_{model}$ = 512 in the original paper varies.
        - How to construct → in section D about word2vec → from one hot encoding to embedding vector → Ex: “Ha” from one hot vector 1 x 32000 → embedding vector 1 x 512 obtained from Word2Vec
    - Output: continuous representation $z = (z_1,..,z_n)$
    - Include components like figure above:
        - first is a multi-head self-attention mechanism
        - second is a simple, position-wise fully connected feed-forward network
        - other: residual connection around each of two sub-layers & layer normalization
- Decoder
    - Input: continuous representation $z = (z_1,..,z_n)$
    - Output: depends on downstream task

### 3; Attention mechanism

- Explain more about the core:
    
    ![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/c6ea46c5-8480-4f92-9aa2-5f7a90ec1326/c26cbe8c-4bf7-4d16-a17b-19eec60fa711/image.png)
    
    - Understanding DL
    - Stanford lectures: https://www.youtube.com/watch?v=LWMzyfvuehA
- Inspiration for Q,K,V: https://stats.stackexchange.com/questions/421935/what-exactly-are-keys-queries-and-values-in-attention-mechanisms
    - Reddit 1: linear projection of the embeddings coming into the "layer" up to a size (q + k + v). The projected vectors are then each split into 3 to produce q, k, and v. So, if there are L words in a sentence, each with a vector embedding, the projection gets you L embeddings each of size (q + k + v).
    - Reddit 2: in the context of the Learning to Align and Translate Paper, it seems that ***"values"*** in this case correspond to ***encoder hidden states***, ***"keys"*** also correspond to ***hidden states***, the ***"output"*** corresponds to the ***context vector*** and ***"query"*** correspond to the ***previous decoder hidden state***.

### 4; Multi-head attention

![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/c6ea46c5-8480-4f92-9aa2-5f7a90ec1326/73a151ca-ad0e-4091-9e12-4b293f581e8c/image.png)

- Q là ma trận encoder ở layer trước output ra
- W_i^Q là ma trận cần nhân chập với Q ở head thứ i
- Visualize: https://jalammar.github.io/illustrated-transformer/

![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/c6ea46c5-8480-4f92-9aa2-5f7a90ec1326/d0f97a33-af7a-4f21-b230-f740401b9817/image.png)

 

# B; BERT

## I; Src tự học

- https://tiensu.github.io/blog/61_bert/
- Code dùng thư viện có sẵn BERT: https://blog.vietnamlab.vn/gioi-thieu-bert-va-ung-dung-vao-bai-toan-phan-loai-van-ban/
- D2L: https://d2l.ai/chapter_natural-language-processing-pretraining/bert.html
- PDK: https://phamdinhkhanh.github.io/2020/05/23/BERTModel.html
- Code giải thích Coursera: [https://github.com/zhang-guodong/Deep-Learning-Specialization/blob/main/Sequence Models/Week 4/C5_W4_A1_Transformer_Subclass_v1.ipynb](https://github.com/zhang-guodong/Deep-Learning-Specialization/blob/main/Sequence%20Models/Week%204/C5_W4_A1_Transformer_Subclass_v1.ipynb)
- Code pure hoàn toàn: https://github.com/jadore801120/attention-is-all-you-need-pytorch/tree/master
- Youtube:
    - https://www.youtube.com/watch?v=-9evrZnBorM&t=616s
    - https://www.youtube.com/watch?v=OR0wfP2FD3c
    - https://www.youtube.com/watch?v=xI0HHN5XKDo&t=216s

## II; Ý tưởng chung

- Encoder of Transformer
    - Input: vector embedding
    - Output: another representation of that vector ($z = (z_1,..,z_n)$)
        - Size: depends on the feed forward fully connected network
- BERT:
    
    ![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/c6ea46c5-8480-4f92-9aa2-5f7a90ec1326/c74a2fdd-9d9e-4057-8d10-43712afd6c44/image.png)
    
    - Input: khác với các câu trong Transformer được convert thành embedding nhờ Word2Vec ⇒ Input của BERT là cặp câu
        - cặp câu cx được convert thành embedding
        - Được thêm thắt 1 số thứ
        
        ![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/c6ea46c5-8480-4f92-9aa2-5f7a90ec1326/9fc4d03b-3ae4-462c-8b1f-406497dd31e6/image.png)
        
        - Các token not word anymore → WordPiece embeddings
    - Output: tùy theo vào từng downstream task
        
        ![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/c6ea46c5-8480-4f92-9aa2-5f7a90ec1326/3a9420fd-5530-4b90-bcaf-9c65c8dc7d75/image.png)
        

## III; Các pha huấn luyện

### 1; Pretrain

- Masked language model
    - to let the model predict missing words based on the surrounding words: mask 15% words (original idea: *Cloze* task in the literature (1953)) → alternative to original bidirectional training ⇒ learn the context without having to forward right and left twice
    - Only apply Masked LM in pretraining process:
        - training data generator chooses 15% of the token positions
        - if i-th token is chosen:
        - (1) the [MASK] token 80% of the time
        - (2) a random token 10% of the time
        - (3) the unchanged i-th token 10% of the time
    - Cụ thể là:
        - Thêm một lớp classification lên trên encoder output
        - Đưa các vector trong encoder ouput về vector bằng với vocab size, sau đó softmax để chọn ra từ tương ứng tại mỗi vị trí trong câu.
        - Loss sẽ được tính tại vị trí masked và bỏ qua các vị trí khác (chỉ để đánh giá xem model dự đoán từ mask đúng/sai, các từ khác không liên quan).
            
            ![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/c6ea46c5-8480-4f92-9aa2-5f7a90ec1326/3ed93959-f1fa-40ef-b377-ba627dc9ef20/image.png)
            
- Next sentence prediction:
    - to let the model learn the relationship between two sentences.
    - Input data: sentence A and sentence B: IsNext & sentence C: NotNext
    - Cụ thể cách train như sau:
        - Bước 1: Ghép 2 câu vào nhau và thêm 1 số token đặc biệt để phân tách các câu. Token [CLS] thêm vào đầu cầu thứ nhất, token [SEP] thêm vào cuối mỗi câu. Ví dụ ghép 2 câu “Hôm nay em đi học” và “Học ở trường rất hay” ⇒ [CLS] Hôm nay em đi học [SEP] Học ở trường rất vui [SEP]
        - Bước 2. Mỗi token trong câu sẽ được cộng thêm một vector gọi là Sentence Embedding, thực ra là đánh dấu xem từ đó thuộc câu thứ nhất hay câu thứ 2 thôi. Ví dụ nếu thuộc câu Thứ nhất thì cộng thêm 1 vector toàn số “0” có kích thước bằng Word Embedding, và nếu thuộc câu thứ 2 thì cộng thêm một vector toàn số “1”.
        - Bước 3. Sau đó các từ trong câu đã ghép sẽ được thêm vector Positional Encoding vào để đánh dấu vị trí từng từ trong câu đã ghép (giống Transformer)
        - Bước 4. Đưa chuỗi sau bước 3 vào mạng.
        - Bước 5. Lấy encoder output tại vị trí token [CLS] được transform sang một vector có 2 phần tử [c1 c2].
        - Bước 6. Tính softmax trên vector đó và output ra probality của 2 class: Đi sau và Không đi sau (câu thứ nhất hay câu thứ hai)
        
        ![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/c6ea46c5-8480-4f92-9aa2-5f7a90ec1326/13792e43-4abf-4f3f-a7d4-927a5f404f4a/image.png)
        

⇒ 2 task này được train đồng thời và loss tổng sẽ là kết hợp loss của 2 task và model sẽ cố gắng minimize loss tổng này

### 2; Finetune

- BERT: uses the self-attention mechanism to unify these two stages (***encode text pairs*** before applying ***bidirectional cross attention*** → common pattern but BERT doesn’t), as encoding a concatenated text pair with self-attention effectively includes bidirectional cross attention between two sentences
- Step 1: For each task, we simply plug in the task specific inputs and outputs into BERT and finetune all the parameters end-to-end.
    - (1) sentence pairs in paraphrasing,
    - (2) hypothesis-premise pairs in entailment,
    - (3) question-passage pairs in question answering
    - (4) a degenerate text-∅ pair in text classification
    or sequence tagging
- Step 2: token representations are fed into an output layer for token level tasks, such as sequence tagging or question answering,
- Step 3: [CLS] representation is fed into an output layer for classification, such as entailment or sentiment analysis.

# C; Phân việc

## I; Các level code có sẵn

- Dùng luôn nn.Transformer → code 15 phút
- Dùng luôn nn.MultiheadAttention
- Chỉ được dùng nn.Embedding
- Không được dùng cả 3 cái trên

## II; Tóm tắt các thành phần chính của Transformer encoder

- ***Word embedding***: use Word2Vec algorithm and already implemented in nn.Embedding
- ***Positional encoding***: implement like the formula in the paper → positional encoding + word embedding = new embedding → fed into multi-head attention
- ***Self-attention*** → got split as multi-head attention
- ***Residual connections*** let the self-attention to focus do its job without remembering about positional encoding

## III; Tóm tắt về BERT

### 1; Tự code hoàn toàn: ý tưởng phân việc

⇒ theo file này (hoặc link Medium gốc: https://medium.com/@alexmriggio/bert-for-sequence-classification-from-scratch-code-and-theory-fb88053800fa)

[Bert_tutorial code on Medium.pdf](https://prod-files-secure.s3.us-west-2.amazonaws.com/c6ea46c5-8480-4f92-9aa2-5f7a90ec1326/94e231bb-e236-4a1c-a45a-0a2316e88c86/Bert_tutorial_code_on_Medium.pdf)

- Người 1: Input representation (code file preprocessing và class Embedding riêng) (11 first pages trong file pdf đính kèm)
    - Convert input text into token —> apply WordPiece tokenization (VD: playing got split → play + ing)
    - Types of embedding and plus together:
        - Original input embedding → created by Word2Vec algorithm, etc → nn.Embedding
        - Segment embedding
        - Positional embedding
    - Tokenization: A **subword tokenization algorithm** is used in the **BERT tokenizer.** Splitting text into subword units strikes a nice balance between vocabulary size and sequence length
        - **WordPiece** is the specific ****subword tokenization algorithm used in the BERT tokenizer
            - Understand thoroughly (optional): https://huggingface.co/learn/nlp-course/chapter6/6?fw=pt
            - Text passed to the BERT tokenizer gets broken down into a sequence of tokens
            - Each unique token in the vocabulary is assigned an integer ID. This acts as a shorthand or abstraction of a one-hot encoded vector.
- Người 2: Multi-head self-attention + feed-forward network after attention (code file Modules.py) (13-28 pages trong file pdf đính kèm)
    
    ![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/c6ea46c5-8480-4f92-9aa2-5f7a90ec1326/51d6dd30-841b-4cde-92cf-36d2ed8ccb6f/image.png)
    
    - code multihead
    - điều chỉnh feed-forward network sao cho phù hợp với downstream-task
    - Add layer normalization, residual connections, position-wise feed-forward networks (feed-forward network in encoder layer is positional-wise)
    - Stack multiple layers
    
    ⇒ Nói chung là complete 1 encoder layer → hoàn thiện để pretrain BERT
    
- Người 3: hoàn thiện BERT + code hàm forward của BERT (loss optimization) (code class BERT và file training.py) (page 28 trong file pdf đính kèm)
    - Có thể xem xét làm thêm gạch đầu dòng 3,4 của người 2 nếu ít task
    - điều chỉnh kiến trúc từ model pretrain sao cho phù hợp downstream task
- Cách làm song song các task:
    - Người 1 → independently
    - Người 2: Trong khi người 1 làm thì dùng tạm input tensor có cùng shape với final output của người 1 (hay như bài gốc có thể là 1 x 512)
        - Cách test thử xem việc mình làm có work không: hiện chưa rõ - trước hết cứ kiểm tra output của ma trận
    - Người 3: dùng tạm module giả (multihead attention, encoder layer giả)
        - Tham khảo cách code: https://neptune.ai/blog/how-to-code-bert-using-pytorch-tutorial

### 2; Sử dụng minBERT: từ BTL của CMU

- Link: https://github.com/neubig/minbert-assignment

![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/c6ea46c5-8480-4f92-9aa2-5f7a90ec1326/99db84ed-e6e1-43bc-9cdd-12bf99d9b376/image.png)

- Người 1:
    - Nếu thầy bắt code lại cả tokenizer → ***code lại giống file tokenizer của họ***
    - Nếu thầy không bắt code lại → tập trung nhiều vào phần tối ưu (KG, knowledge injection,…)
- Người 2:
    - Đọc hiểu paper BERT + file bert-base.py
    - ***Hoàn thành file bert.py***
- Người 3:
    - ***Hoàn thành file classifier.py***
    - Tìm hiểu xem có dùng được AdamW có sẵn của PyTorch k → k thì code lại

### 3; Sử dụng minBERT: từ BTL của Stanford

- Link: https://github.com/lry00127/miniBert
    
    ![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/c6ea46c5-8480-4f92-9aa2-5f7a90ec1326/0380007f-d007-4831-9198-e1c44928af56/image.png)
    
- Người 1:
    - ***Hoàn thành file [tokenizer.py](http://tokenizer.py) và bert.py***
- Người 2:
    - ***Hoàn thành file classifier.py***
    - Làm nhiều phần knowledge injection
- Người 3:
    - ***Hoàn thành file multitask_classifier.py***

### 4; Ước tính thời gian huấn luyện

- Trong paper gốc
    
    ![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/c6ea46c5-8480-4f92-9aa2-5f7a90ec1326/9d1c8d37-58ee-4341-8c83-1857925afbfa/image.png)
    
- Từ các nguồn khác

![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/c6ea46c5-8480-4f92-9aa2-5f7a90ec1326/21ccec91-8cb4-4de1-8c8c-135b24edb755/image.png)

- minBERT của CMU: không có thông tin
- minBERT của Stanford:
    
    ![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/c6ea46c5-8480-4f92-9aa2-5f7a90ec1326/a050d29c-8483-4bde-bfa4-e05440ea933c/image.png)
    
    ⇒ nhiều miniproject: thường mất 1 ngày để pretrain → debug blah blah chắc nên ít nhất 3 tuần trước deadline
    
    ⇒ List mini projects:
    
    - https://web.stanford.edu/class/archive/cs/cs224n/cs224n.1244/final-projects/IshitaMangla.pdf
    - https://web.stanford.edu/class/archive/cs/cs224n/cs224n.1244/final-projects/QianZhong.pdf
    - https://web.stanford.edu/class/archive/cs/cs224n/cs224n.1244/final-projects/LongDPham.pdf
    - https://web.stanford.edu/class/archive/cs/cs224n/cs224n.1234/final-reports/final-report-169514243.pdf
    - https://web.stanford.edu/class/archive/cs/cs224n/cs224n.1244/final-projects/MadhumitaVijayDangeYuwenYang.pdf
    - https://web.stanford.edu/class/archive/cs/cs224n/cs224n.1234/final-reports/final-report-169500618.pdf
    - https://web.stanford.edu/class/archive/cs/cs224n/cs224n.1244/final-projects/MadhumitaVijayDangeYuwenYang.pdf
    - https://web.stanford.edu/class/archive/cs/cs224n/cs224n.1234/final-reports/final-report-169319223.pdf
    - https://web.stanford.edu/class/archive/cs/cs224n/cs224n.1244/final-projects/RahulThapaRohitKhurana.pdf
    - https://web.stanford.edu/class/archive/cs/cs224n/cs224n.1234/final-reports/final-report-169724933.pdf
    - https://web.stanford.edu/class/archive/cs/cs224n/cs224n.1234/final-reports/final-report-169997382.pdf
    - https://arxiv.org/html/2407.14039v1

# D; Các kiến thức khác

## I; Một số chỉ số đánh giá model

- GLUE
- BLEU

⇒ Tạm thời để sau cho tới khi chốt được task chính huấn luyện BERT

## II; Một số kiến thức khác

- Word2Vec: https://machinelearningcoban.com/tabml_book/ch_embedding/word2vec.html

## III; Performance của BERT sau khi finetuning trên 1 số bài toán trong paper gốc

- Nhiều metric + nhiều dataset đánh giá → tạm thời để sau cho tới khi chốt được task chính huấn luyện BERT
- Stanford’s base code:
    - sentiment classification.
    - paraphrase detection
    - semantic similarity.
- CMU’s base code:
    - ***CFIMDB*** datasets: IMDB Dataset of 50K Movie Reviews
    - SST datasets: Stanford Sentiment Treebank
