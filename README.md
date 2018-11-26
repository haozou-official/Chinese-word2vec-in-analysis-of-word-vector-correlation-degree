# Chinese-word2vec-in-analysis-of-word-vector-correlation-degree
Chinese word2vec in analysis of word vector correlation degree in the famouse novel The Heaven Sword and Dragon Saber By Jin Yong
# 1.Do the word segmentation of the corpus as the corpus of the training model
```
def cut_txt(old_file):
    import jieba
    global cut_file     # 分词之后保存的文件名
    cut_file = old_file + '_cut.txt'

    try:
        fi = open(old_file, 'r', encoding='utf-8')
    except BaseException as e:  # 因BaseException是所有错误的基类，用它可以获得所有错误类型
        print(Exception, ":", e)    # 追踪错误详细信息
```
# 2.Remove punctuation and spaces
    text = fi.read()  # 获取文本内容
    new_text = jieba.cut(text, cut_all=False)  # 精确模式
    str_out = ' '.join(new_text).replace('，', '').replace('。', '').replace('？', '').replace('！', '') \
        .replace('“', '').replace('”', '').replace('：', '').replace('…', '').replace('（', '').replace('）', '') \
        .replace('—', '').replace('《', '').replace('》', '').replace('、', '').replace('‘', '') \
        .replace('’', '')     # 去掉标点符号
    fo = open(cut_file, 'w', encoding='utf-8')
    fo.write(str_out)
# 3.word2vec model calls
# 4.Training Models
```
logging.basicConfig(format='%(asctime)s : %(levelname)s : %(message)s', level=logging.INFO)
sentences = word2vec.Text8Corpus(train_file_name)  # 加载语料
model = gensim.models.Word2Vec(sentences, size=200)  # 训练skip-gram模型; 默认window=5
model.save(save_model_file)
model.wv.save_word2vec_format(save_model_name + ".bin", binary=True)   # 以二进制类型保存模型以便重用
```
# 5.Load a trained model
```
model_1 = word2vec.Word2Vec.load(save_model_name)
```
# 6.Calculate the similarity of two words
```
赵敏和韦一笑的相似度为： 0.7938857
```
# 7.Calculate a list of related words for a word
```
和张三丰最相关的词有：

金花婆婆 0.9892849922180176
张松溪 0.9846320152282715
四弟 0.9816751480102539
赵敏格 0.9814869165420532
可行 0.9795811176300049
事不宜迟 0.9795102477073669
灭绝师太 0.9793342351913452
寿南山 0.978480339050293
通道 0.977789580821991
宋远桥 0.9776178002357483
```
