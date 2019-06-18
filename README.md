# Shakespearizing-Modern-English
Code for "Jhamtani H., Gangal V., Hovy E. and Nyberg E. Shakespearizing Modern Language Using Copy-Enriched Sequence to Sequence Models"  Workshop on Stylistic Variation, EMNLP 2017

Code has been tested with Tensorflow version 1.1.0
- If you use this code or the processed data, please consider citing Jhamtani H., Gangal V., Hovy E. and Nyberg E. Shakespearizing Modern Language Using Copy-Enriched Sequence to Sequence Models"  Workshop on Stylistic Variation, EMNLP 2017
- If you use the data, please consder citing "Wei Xu, Alan Ritter, William B Dolan, Ralph Grish- man, and Colin Cherry. 2012. Paraphrasing for style. In 24th International Conference on Computational Linguistics, COLING 2012."

Instructions to run: </br>
Preprocessing:
```bash
cd code/main/
mkdir tmp
python mt_main.py preprocessing
```

Pointer model: 
- First run pre-processing, then run training:
```bash
cd code/main/
python mt_main.py train 10 pointer_model
```
Inference:
```bash
cd code/main/
python mt_main.py inference tmp/pointer_model7.ckpt greedy
```

Normal seq2seq model: 
- First run pre-processing
```bash
cd code/main/
python mt_main.py train 10 seq2seq
```
For inference:
```bash
cd code/main/
python mt_main.py inference tmp/seq2seq5.ckpt greedy
```

Post-Processing:
There are two post-processing actions which one may be interested in performing:
1. Visualizing attention matrices
2. Replacing UNKS in hypothesis with their highest-aligned (attention) input tokens.
For both of these actions, refer to the running instructions in code/main/post_process.py (comments commencing the file). The file can be run in two modes, to perform 1 (write) and 2 (postProcess) respectively*.
*Not elaborated on here to preserve conciseness and clarity.


Baseline (Dictionary):
- Change working directory to code/baselines/
- python dictionary_baseline.py ../../data/shakespeare.dict ../../data/test.modern.nltktok ../../data/test.dictBaseline
- The test.dictBaseline file contains the output (Shakespearean) of the dictionary baseline.
- To evaluate BLEU: 
  - Change working directory to code/main/
  - perl multi-bleu.perl -lc ../../data/test.original.nltktok < ../../data/test.dictBaseline

Baseline (statistical MT)
- Please follow instructions in "Wei Xu, Alan Ritter, William B Dolan, Ralph Grish- man, and Colin Cherry. 2012. Paraphrasing for style. In 24th International Conference on Computational Linguistics, COLING 2012."
