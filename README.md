# Vison-Transformer
学习笔记，大佬勿喷
##
Vision Transformer作用是将image映射为visual_token_embedding，是CLIP等多模态模型的必要组件
##
主要使用Transformer框架的encoder部分，类似于Bert等给text编码为embedding的模型，但实现重点在如何将image视为text？
##
原文用的是DNN法，即将图像视为n个大小完全相同且无像素重叠的patch，每个patch都将编码为一个embedding。在与线性变换权重相乘之前的表示维度上，dim=2的部分维度=patch块中像素个数=patch_size*patch_size*input_channel
##
也可以用CNN法实现，也就是将其卷积核定义为与patch_size相同的尺寸，且output_channel=d_model
##
后续将得到的embedding加上类监督标签cls，其也可视为该图像的一个patch，因此concat所在维度应为dim=1。（这里原文说各方法效果都差不多,所以cls随机初始化后续可训练优化）
##
再加上位置编码，其中注意保持维度一致
##
最后可取出mlp_head的最后一层表示做交叉熵分类


