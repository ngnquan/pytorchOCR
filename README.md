## OCR library based on pytorch

This link is for person which is new to OCR [CSDN Blog](https://blog.csdn.net/fxwfxw7037681/category_10419715.html)

***
Recently updated:
- 2020.12.22 Update CRNN+CTCLoss + CenterLoss training
- 2020.09.18 Update text detection documentation
- 2020.09.12 Update DB,pse,pan,sast,crnn Training test code and pre-trained model

***
Currently completed:

- [x] DBnet [Paper link](https://arxiv.org/abs/1911.08947)
- [x] PSEnet [Paper link](https://arxiv.org/abs/1903.12473)
- [x] PANnet [Paper link](https://arxiv.org/pdf/1908.05900.pdf)
- [x] SASTnet [Paper link](https://arxiv.org/abs/1908.05498)
- [x] CRNN [Paper link](https://arxiv.org/abs/1507.05717)
***
Next plan：

- [x] Model transfer onnx and test
- [x] Model compression (pruning)
- [ ] Model compression (quantization)
- [x] Model distillation
- [x] Deploy tensorrt
- [ ] Training generalized OCR model
- [ ] Deploy with chinese_lite
- [ ] Mobile deployment
***
### Detect model result (in experiment)

The training is only on the ICDAR2015 text detection public data set, and the algorithm result is as follows:
|Model|Backbone Network|Precision|Recall|Hmean|Download Link|
|-|-|-|-|-|-|
|DB|ResNet50_7*7|85.88%|79.10%|82.35%|[Download link](https://pan.baidu.com/s/1zONYFPsS3szaf5BHeQh5ZA)(code:fxw6)|
|DB|ResNet50_3*3|86.51%|80.59%|83.44%|[Download link](https://pan.baidu.com/s/1zONYFPsS3szaf5BHeQh5ZA)(code:fxw6)|
|DB|MobileNetV3|82.89%|75.83%|79.20%|[Download link](https://pan.baidu.com/s/1zONYFPsS3szaf5BHeQh5ZA)(code:fxw6)|
|SAST|ResNet50_7*7|85.72%|78.38%|81.89%|[Download link](https://pan.baidu.com/s/1zONYFPsS3szaf5BHeQh5ZA)(code:fxw6)|
|SAST|ResNet50_3*3|86.67%|76.74%|81.40%|[Download link](https://pan.baidu.com/s/1zONYFPsS3szaf5BHeQh5ZA)(code:fxw6)|
|PSE|ResNet50_7*7|84.10%|80.01%|82.01%|[Download link](https://pan.baidu.com/s/1zONYFPsS3szaf5BHeQh5ZA)(code:fxw6)|
|PSE|ResNet50_3*3|82.56%|78.91%|80.69%|[Download link](https://pan.baidu.com/s/1zONYFPsS3szaf5BHeQh5ZA)(code:fxw6)|
|PAN|ResNet18_7*7|81.80%|77.08%|79.37%|[Download link](https://pan.baidu.com/s/1zONYFPsS3szaf5BHeQh5ZA)(code:fxw6)|
|PAN|ResNet18_3*3|83.78%|75.15%|79.23%|[Download link](https://pan.baidu.com/s/1zONYFPsS3szaf5BHeQh5ZA)(code:fxw6)|
***
### Model compression pruning result

Here, mobilev3 is used as the backbone. As a result of testing on icdar2015, the initial size of the uncompressed model is 2.4M.

1. Compress the backbone

|Model|Pruned method|Ratio|Model size(M)|Precision|Recall|Hmean
|-|-|-|-|-|-|-|
|DB|no|0|2.4|84.04%|75.34%|79.46%|																																																						
|DB|backbone|0.5|1.9|83.74%|73.18%|78.10%|
|DB|backbone|0.6|1.58|84.46%|69.90%|76.50%|

2. Compress the entire model

|Model|pruned method|ratio|model size(M)|precision|recall|Hmean|
|-|-|-|-|-|-|-|
|DB|no|0|2.4|85.70%|74.77%|79.86%|
|DB|total|0.6|1.42|82.97%|75.10%|78.84%|
|DB|total|0.65|1.15|85.14%|72.84%|78.51%|
***
### Model distillation

|Model|Teacher|Student|Model size(M)|Precision|Recall|Hmean|Improve(%)|
|-|-|-|-|-|-|-|-|
|DB|no|mobilev3|2.4|85.70%|74.77%|79.86%|-|
|DB|resnet50|mobilev3|2.4|86.37%|77.22%|81.54%|1.68|
|DB|no|mobilev3|1.42|82.97%|75.10%|78.84%|-|
|DB|resnet50|mobilev3|1.42|85.88%|76.16%|80.73%|1.89|
|DB|no|mobilev3|1.15|85.14%|72.84%|78.51%|-|
|DB|resnet50|mobilev3|1.15|85.60%|74.72%|79.79%|1.28|
***


### Documentation tutorial
- [Text detection](./doc/md/文本检测训练文档.md)
- [Text recognition](./doc/md/文本识别训练文档.md)
- [pytorch to onnx](./doc/md/pytorch_to_onnx.md)
- [onnx to tensorrt](./doc/md/onnx_to_tensorrt.md)
- [Model pruning](./doc/md/模型剪枝.md)
- [Model distillation](./doc/md/模型蒸馏.md)




***

### Text detection result
<img src="./doc/show/ocr1.jpg" width=600 height=600 />     
<img src="./doc/show/ocr2.jpg" width=600 height=600 />

***

### Questions and exchanges plus WeChat

WeChat number: -fxwispig-
***


### Reference

- https://github.com/PaddlePaddle/PaddleOCR
- https://github.com/whai362/PSENet
- https://github.com/whai362/pan_pp.pytorch
- https://github.com/WenmuZhou/PAN.pytorch
- https://github.com/xiaolai-sqlai/mobilenetv3
- https://github.com/BADBADBADBOY/DBnet-lite.pytorch
- https://github.com/BADBADBADBOY/Psenet_v2
- https://github.com/BADBADBADBOY/pse-lite.pytorch