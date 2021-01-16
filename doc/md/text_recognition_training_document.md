### Text recognition
#### Tata preparation

Need one file train_list.txt [example](https://github.com/BADBADBADBOY/pytorchOCR/blob/master/doc/example/rec_train_list.txt) , Format: Picture absolute path+\t+label. For details, please refer to the example in data/example in the project.
If you need to do verification during training, you need to make the same data format. There is a test_list.txt [example](https://github.com/BADBADBADBOY/pytorchOCR/blob/master/doc/example/rec_test_list.txt)

#### Normal training model (take rec_CRNN_ori.yaml as an example)
1. Set restore and finetune under base in yaml to False, use_center under loss to False, modify the data path and other parameters.
2. Run the following command

```
python3 ./tools/rec_train.py --config ./config/rec_CRNN_ori.yaml --log_str log


#### CenterLoss Training model (take rec_CRNN_ori.yaml as an example)
1. Set restore and finetune under base in yaml to True, use_center under loss to True, and assign the optimal model file address obtained from normal training to restore_file under base.
2. Run the following command

```
python3 ./tools/rec_train.py --config ./config/rec_CRNN_ori.yaml --log_str log
```
#### Test model
1. Assign the trained model to model_path under infer in yaml, and assign the image address to path
2. Run the following command

```
python3 ./tools/rec_infer.py
```