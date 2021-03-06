# Saliency detection by multi-context deep learning

基于多上下文深度学习的显著性检测

显著性检测(Saliency detection)旨在突出图像中视觉上显著的区域或物体

![image-20211213170633028](C:\Users\10141\AppData\Roaming\Typora\typora-user-images\image-20211213170633028.png)

局部是分开考虑两个红框，都显著。全局的话花比叶显著，车比栏杆显著。

本文的工作是设计一个具有多个上下文的深度模型来捕获对象的显著性。在全图像中，利用全局上下文对显著性进行建模，而在精细区域中，利用局部上下文进行显著性预测。将全局和局部上下文整合到多上下文深度学习框架中进行显著性检测，并对全局和局部上下文建模进行联合优化。



文章模型如下图

![image-20211213172004712](C:\Users\10141\AppData\Roaming\Typora\typora-user-images\image-20211213172004712.png)

其中卷积层用蓝色表示，完全连接层(参数使用预先训练的模型参数初始化)用橙色表示，完全连接层(参数随机初始化)用红色表示。图中省略了没有参数的层。