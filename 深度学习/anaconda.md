anaconda管理包

## anaconda

```python
//创建pytorch环境
conda create -n pytorch python=3.6
//切换pytorch环境
conda activate pytorch
//根据自己的版本下载的
conda install pytorch torchvision torchaudio pytorch-cuda=12.1 -c pytorch -c nvidia


//输入python
//进入python编译器界面
import torch
torch.cuda.is_available()

//pytorch下载jupyter notebook
//因为下载的是base环境下，所以再pytorch没有再下一遍
conda activate pytorch
conda install nb_conda

```



## pytorch两大法宝

```
dir();打开，看见
help();说明书
```





![image-20231205210738779](C:\Users\30992\Desktop\编程注意\picture\image-20231205210738779.png)

Dataset

Dataloader

### 终端修改

![image-20231205212701197](C:\Users\30992\Desktop\编程注意\picture\image-20231205212701197.png)

![image-20231205212653192](C:\Users\30992\Desktop\编程注意\picture\image-20231205212653192.png)



## tensorboad

pip install tensorboard

运行出现logs文件

tensorboard --logdir=logs

打开tensorboard命令行

tensorboard --logdir=logs --port=6007

打开指定端口

```python
from torch.utils.tensorboard import SummaryWriter
import numpy as np
from PIL import Image

writer = SummaryWriter("logs")
image_path = "hymenoptera_data/train/ants_image/0013035.jpg"
img_PIL = Image.open(image_path)
img_array = np.array(img_PIL)
writer.add_image("test", img_array, 1, dataformats='HWC')
# writer.add_scalar()
for i in range(100):
    writer.add_scalar("y=2x", 2 * i, i)

writer.close()
```



## transforms.py工具箱



![image-20231206203714714](C:\Users\30992\Desktop\编程注意\picture\image-20231206203714714.png)

![image-20231206204656127](C:\Users\30992\Desktop\编程注意\picture\image-20231206204656127.png)

totensor

resize

## sklearn库

pip install scikit-learn