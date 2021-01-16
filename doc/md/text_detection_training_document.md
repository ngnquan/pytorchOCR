## Training document
***

### Step 1: Environment installation and pre-training model
1. Process files after compiling c++

```
sh make.sh
```
2. Download the pre-trained model
Pre-training model address: [Download link](https://pan.baidu.com/s/1zONYFPsS3szaf5BHeQh5ZA)(code:fxw6)

3. Download the icdar2015 test model (you can skip this step if you don't do the test)
Test model：[Download link](https://pan.baidu.com/s/1zONYFPsS3szaf5BHeQh5ZA)(code:fxw6)

4. Replace the downloaded pre_model and checkpoint folders with the folders of the same name in the project
***

### Step 2: Prepare training documents
1.Prepare one train_list.txt[Example](https://github.com/BADBADBADBOY/pytorchOCR/blob/master/doc/example/det_train_list.txt). The format is: the absolute position of the picture file + the absolute position of the picture file marked txt file, separated by \t. Refer to the following and modify it to your own address.

```
python3 ./script/get_train_list.py --img_path /src/train/image --label_path /src/train/label --save_path /src/train
```
After running /src/train will generate one file train_list.txt.
- Tip: Your image and label file should have the same name. If you want to do verification during training, you need to generate a file test_list.txt[Example](https://github.com/BADBADBADBOY/pytorchOCR/blob/master/doc/example/det_test_list.txt). How many epochs can be set in start_val in yaml to start verification.
- Instructions for making label files: follow the format of icdar2015: x1,y1,x2,y2,x3,y3,x4,y4,label. Which does not participate in the training text (for example, fuzzy text), the label is set to ###, which means not to participate in the training, otherwise it means to participate in the training, you can use text like me, Or something else will do. [label format refer to here](https://github.com/BADBADBADBOY/pytorchOCR/blob/master/doc/example/label.txt)
***
### Step 3: Model training
#### Normal model training

1. To modify the yaml parameters of the corresponding algorithm in ./config, basically you only need to modify the data path.
2. Run the following command

```
python3 tools/det_train.py --config ./config/det_DB_mobilev3.yaml --log_str train_log  --n_epoch 1200 --start_val 600 --base_lr 0.002 --gpu_id 2
```

- Típ: In ./config/det_DB_resnet50.yaml inside [Parameter explanation](https://github.com/BADBADBADBOY/pytorchOCR/blob/master/config/det_DB_resnet50.yaml). Other yaml files are similar, you can refer to them. log_str is to save the results in different folders when training multiple times

#### Breakpoint recovery training
Set restore under base in the yaml file to True, fill in the address of the restored training model in restore_file, and run：
```
python3 tools/det_train.py --config ./config/det_DB_mobilev3.yaml --log_str train_log  --n_epoch 1200 --start_val 600 --base_lr 0.002 --gpu_id 2
```


***

### Step 4: Model test
1. Modify the parameters in infer.sh
2. Run the following command

```
sh infer.sh
```
-Tip: During the test, the --img_path in the infer.sh file can be either a folder or a file




