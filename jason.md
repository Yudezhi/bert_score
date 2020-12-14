# BERTScore 使用说明

## 相关说明

* 如果用命令行之前还是要把terminal proxy 设置一下
* 查看各个模型的性能： [谷歌表格](https://docs.google.com/spreadsheets/d/1RKOVpselB98Nnh_EOC4A2BYn8_201tmPODpNWu4w7xI/edit#gid=0)
* 支持的语言： [语言列表](https://github.com/google-research/bert/blob/master/multilingual.md#list-of-languages)
* 所有模型下载地址： [模型下载页面](https://huggingface.co/models)
* 不同的模型出现的结果大有不同
* 英文单词的大小写竟然影响相似度

## 常用指令

#### 中文句子评分

```bash
bert-score -r "好的" -c "不行" --model C:\Users\Bobing\Desktop\bert_score\models\bert-base-chinese --num_layers 9 [--lang zh]

```

#### 两个文件评分

```bash
bert-score -r example/refs.txt -c example/hyps.txt --lang en
```

#### 指定模型评分

```bash
bert-score -r example/refs.txt -c example/hyps.txt --model C:\Users\Bobing\Desktop\bert_score\models\roberta-large --num_layers 9
```

#### 多个参考句子的评分

```bash
bert-score -r example/refs.txt example/refs2.txt -c example/hyps.txt --lang en
```

#### 可视化两个句子的相关性

```bash
bert-score-show --lang en -r "There are two bananas on the table." -c "On the table are two apples." -f out.png
```

### bert-score -h

```bash
usage: Calculate BERTScore [-h] [--lang LANG] [-m MODEL] [-l NUM_LAYERS]
                           [-b BATCH_SIZE] [--nthreads NTHREADS] [--idf]
                           [--rescale_with_baseline]
                           [--baseline_path BASELINE_PATH] [-s] [-v] -r REF
                           [REF ...] -c CAND

optional arguments:
  -h, --help            show this help message and exit
  --lang LANG           two-letter abbreviation of the language (e.g., en) or
                        "en-sci" for scientific text
  -m MODEL, --model MODEL
                        BERT model name (default: bert-base-uncased) or path
                        to a pretrain model
  -l NUM_LAYERS, --num_layers NUM_LAYERS
                        use first N layer in BERT (default: 8)
  -b BATCH_SIZE, --batch_size BATCH_SIZE
                        batch size (default: 64)
  --nthreads NTHREADS   number of cpu workers (default: 4)
  --idf                 BERT Score with IDF scaling
  --rescale_with_baseline
                        Rescaling the numerical score with precomputed
                        baselines
  --baseline_path BASELINE_PATH
                        path of custom baseline csv file
  -s, --seg_level       show individual score of each pair
  -v, --verbose         increase output verbosity
  -r REF [REF ...], --ref REF [REF ...]
                        reference file path(s) or a string
  -c CAND, --cand CAND  candidate (system outputs) file path or a string
```
