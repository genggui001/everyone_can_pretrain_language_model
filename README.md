Everyone Can Pretrain Language Model
===========================
一份白嫖colab与kaggle的TPU预训练语言模型的指南，没钱也能训练个bert-base玩玩

其中语言模型的代码均采用苏神的[bert4keras](https://github.com/bojone/bert4keras)

注：求在TPU上使用过重计算的大佬帮助，求TPU重计算的参考代码

****

## 白嫖前的准备工作

1. colab或者kaggle账号一个，kaggle需要验证手机才能用TPU
2. google cloud账号一个，使用其中的google storage来保存语言模型的训练数据，免费300刀试用3个月，需要visa或者万事达卡一张，比较麻烦，愿意折腾的可以尝试浦发银行的虚拟visa，无限申请，或者购买老版300美金试用1年的账号
3. 一个速度快的科学上网工具（非必须），没有的话就推荐使用国外的机器进行数据预处理并上传
4. google edu 教育邮箱一个，可从淘宝购买，colab用户可以更加方便的保存参数

------

## 新建Google Storage存储分区，并设置访问权限
1. 进入[Google Storage](https://console.cloud.google.com/storage/)并创建一个新存储分区

![upload_1](images/upload_1.png)

2. 数据存储位置先选 Dual-region 再选 eur4 (荷兰和芬兰) (免费TPU都在欧洲)

![upload_2](images/upload_2.png)

3. 给新的存储分区增加公共读权限（可能会不安全，求大佬推荐更加安全的做法）

![upload_3](images/upload_3.png)

------

## 数据预处理

预处理代码请自行参考苏神的[pretraining/data_utils.py](https://github.com/bojone/bert4keras/blob/master/pretraining/data_utils.py)

得到一个或者数个corpus.xxx.tfrecord的文件

------

## 数据上传

三种方式：

1. 在浏览器中上传（应该不用截图吧），好的科学上网工具都能有100Mbs，可以接受
2. rclone 挂载 google storage 后上传，需要国外机器，可参考[rclone官方指南](https://rclone.org/googlecloudstorage/)
3. 直接用 colab 生成到 google storage 里面（以后补充，应该可行）

------

## 采用 Colab TPU 训练

TPU型号：TPU v2-8 64G

语言模型定义：bert4keras

训练数据：Google Storage中之前上传的corpus.xxx.tfrecord

参数保存：Google Drive中某个指定的文件夹

1. 上传训练代码[colab_pretrain.ipynb](colab_pretrain.ipynb)，并根据注释修改

2. 设置运行环境为TPU

![run_1](images/run_1.png)
![run_2](images/run_2.png)

3. 运行代码，挂载谷歌网盘

![run_3](images/run_3.png)

4. F12控制台内输入自动点击代码，防止掉线

![run_4](images/run_4.png)

```
function ConnectButton(){
    console.log("Connect pushed"); 
    document.querySelector("#top-toolbar > colab-connect-button").shadowRoot.querySelector("#connect").click();
}
setInterval(ConnectButton,60000);
```

5. 12小时（Pro版本 24小时）后来重新运行代码，继续训练

### 需要注意的点：

1. 需要google edu的无限网盘，不然bert的参数可以直接耗光你的15G存储空间（可能以后会出存放在google storage的版本）

2. 当前的谷歌TPU的TF版本为2.4，不保证以后能一直用

3. Colab的控制台输出可能会出现超出buffer size的问题，但不影响训练，只是进度条不更新，可以去保存的路径下查看保存的参数文件

------

## 采用 Kaggle TPU 训练

TPU型号：TPU v3 128G

语言模型定义：bert4keras

训练数据：Google Storage

参数保存：Google Storage

咕咕咕(Todo)






