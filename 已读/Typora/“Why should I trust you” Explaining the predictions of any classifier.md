# “Why should I trust you” Explaining the predictions of any classifier

这篇文章主要讲述了一种**解释模型预测方法LIME**，让人们能够理解模型背后的基本原理，有助于辅助用户什么时候信任或者不信任一个模型的预测。

------

## 为什么我们需要解释器？

在进行机器学习的相关工作时，我们经常依据其prediction的精度来选择是否信任一个模型，**但是我们能否选择信任这个预测结果，或者信任这个模型做出的判断**。

说服别人：在我们使用机器学习的方法来帮助专业人士进行判断时，比如医生、法律这种十分重视理由的专业，不能仅仅说“模型是这样说的”就结束了，我们需要通过解释器去了解模型背后的原理，以此来说服别人。
说服自己：在建立模型后，通过样本的可解释性帮助人类进行判断，模型是否真正学到了我们所预期的事情。
论文中有一组实验可以很好的说明为何我们需要解释器，下面一组图片展示了某分类器将哈士奇识别成了狼，我们的第一反应也许是分类器发生了误判，毕竟模型本身不可能百分百正确。这时我们希望出现图2所示的分类器，来告诉我们为什么这个样本被识别成狼，此时分类器解释：“因为这张图片除了本体之外都是白色的雪地，因此模型把该图片分类成狼”。 
![image-20211222071220844](C:\Users\10141\AppData\Roaming\Typora\typora-user-images\image-20211222071220844.png)

![image-20211222071233395](C:\Users\10141\AppData\Roaming\Typora\typora-user-images\image-20211222071233395.png)

从上面的例子我们可以发现，在样本的刻意选取下，模型学习到了只要背景是白色的（雪地），就很可能识别为狼，反之背景不是白色的，那就很可能是哈士奇。这样的学习结果肯定不是我们想要模型去学习的内容。这也是我们需要一个解释器这样的角色，来选择是否信任模型做出的判断。

------

## 解释器的基础特征

身为一个解释器，文中要求至少满足以下特征： 
 ·可解释性（Interpretable） 
 ·局部忠诚（Local Fidelity） 
 ·与模型无关（Model-Agnostic） 
 ·全局视角（Global Perspective） 

**可解释性**：包含两个部分，分别为模型和特征。我们以模型为例，像决策树或是线性回归都是很适合拿来解释的模型，前提是特征也要容易解释才行。

**局部忠诚**：既然我们已经使用了可解释的模型与特征，就不可能期望简单的可解释模型在效果上等同于复杂模型（比如原始CNN分类器）。所以解释器不需要在全局上达到复杂模型的效果，但至少在局部上效果要很接近，而此处的局部代表我们想观察的那个样本的周围。

**与模型无关**：这里所指的是与复杂模型无关，换句话说无论多复杂的模型，像是SVM或神经网络，该解释器都可以工作。

**全局视角**：准确度有时并不是一个很好的指标，提供一个全局的视角对于确定模型的可信度也很重要。

------

## LIME方法介绍

解释器的目的：**“对于一个分类器（复杂模型），想用一个可解释的模型（简单模型如线性规划），搭配可解释的特征进行适配，并且这个可解释模型再局部的表现上很接近复杂模型的效果”。**

LIME的全称为：Local Interpretable Model-Agnostic Explanation，中文字面上的意思就是与模型无关的局部可解释性的解释。LIME通过扰动输入样本（perturb the input），来判断哪些特征的存在与否，对于输出结果有着最大的影响。而扰动的精髓在于这些绕扰动必须是人类可以理解的。像是一张图片中，将图片中的部分区域进行遮盖，对识别效果肯定是有一定影响的；
LIME目标函数如下

![image-20211222075115991](C:\Users\10141\AppData\Roaming\Typora\typora-user-images\image-20211222075115991.png)

![image-20211222075254817](C:\Users\10141\AppData\Roaming\Typora\typora-user-images\image-20211222075254817.png)

设L(f, g，πx)为g在由πx定义的位置上近似f的不忠实程度的测度。还有一部分公式把Πx换了，这里没有贴出来。

------

举一些例子

![image-20211222075855706](C:\Users\10141\AppData\Roaming\Typora\typora-user-images\image-20211222075855706.png)

![image-20211222080550688](C:\Users\10141\AppData\Roaming\Typora\typora-user-images\image-20211222080550688.png)

![image-20211222080624639](C:\Users\10141\AppData\Roaming\Typora\typora-user-images\image-20211222080624639.png)