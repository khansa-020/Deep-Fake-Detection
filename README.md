# Deep-Fake-Detection
Comparative analysis of ML and DL techniques for Deep Fake Detection using efficientNetB3 as framework or baseline
| Model                     | Pretrained     | Fine-tuned | Combined? | Notes                 |
| ------------------------- | -------------- | ---------- | --------- | --------------------- |
| Simple CNN                | No             | No         | No        | Basic baseline        |
| InceptionV3               | Yes (ImageNet) | Yes        | No        | Transfer learning     |
| InceptionV3 + DenseNet121 | Yes            | Yes        | Yes       | Feature fusion hybrid |
| EfficientNet-B3           | Yes (ImageNet) | Yes        | No        | Proposed final model  |
