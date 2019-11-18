# TensorFlow工具的编译和使用
TensorFlow工具是TensorFlow框架用来训练和导图的。

## 准备

###　安装bazel工具
参考这个文档安装bazel，1.0以上的版本会报错，确认可使用的版本号为0.29.1.[编译安装bazel](/ubuntu/ubuntu-development0002-bazel.html)

### 获取TensorFlow源码
先安装git工具
```bash
$ sudo apt update
$ sudo apt install git
```
从TensorFlow的git仓库拉取
```bash
$ git clone https://github.com/tensorflow/tensorflow.git
```

## 编译

### freeze_graph工具
freeze_graph工具用于冻结导出的graph。
```bash
$ bazel build tensorflow/python/tools:freeze_graph
```
编译过程会非常漫长，这与你的cpu内存以及线程数有关。

### summarize_graph工具
summarize_graph工具用于查看graph的信息
```bash
$ bazel build tensorflow/tools/graph_transforms:summarize_graph
```
编译过程同样比较漫长

### label_image示例
label_image是c/c++接口的一个示例文件，可用于初步检验训练结果
```bash
$ bazel build tensorflow/examples/label_image:label_image
```

## 使用
下面的使用示例中graph可以使用你自己的graph，修改路径就可以，我这里的是由[使用TensorFlow训练inception模型](/AI/ai-examples0001-tf-inception.html)训练出来的数据。

### freeze_graph工具使用
```bash
$ python ~/tensorflow/tensorflow/tensorflow/python/tools/freeze_graph.py \
  --input_graph=/tmp/inception_v3_inf_graph.pb \
  --input_checkpoint=/tmp/train_log/inception_v3_retrain/model.ckpt-66505 \
  --input_binary=true --output_graph=/tmp/frozen_inception_v3.pb \
  --output_node_names=InceptionV3/Predictions/Reshape_1
```

> 1. 编译出来以后无法直接找到freeze_graph工具，使用的是相应的python脚本
> 2. 参数 
> `--input_graph`           需要冻结的graph
> `--input_checkpoint`      输入的checkpoint
> `--output_graph`          输出的冻结后的graph的位置
> `--output_node_names`     输出的节点的名称

### summarize_graph工具
```
$ bazel-bin/tensorflow/tools/graph_transforms/summarize_graph \
  --in_graph=/tmp/inception_v3_inf_graph.pb
```
> 参数 `--in_graph`         输入的需要读取graph信息的graph

### label_image示例

```bash
$ python tensorflow/examples/label_image/label_image.py --graph /tmp/frozen_inception_v3.pb \
		--labels /path/to/labels.txt \ 
		--image  /path/to/image.jpg
```
> 参数
> `--graph`       graph的位置
> `--labels`      labels.txt文件的位置
> `--image`       输入的图片位置



