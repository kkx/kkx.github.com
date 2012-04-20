---
layout: post
title: "根据bag of keypoints图片分类"
date: 2012-04-20 02:41
comments: true
categories: 计算机视觉 图像 分类
---

最近看了一篇名叫[Categorizing nine visual classes using local appearance descriptors] 的论文，相当受启发，该论文以Information retrieval里[bag of words]\(以单词的出现的次数的矩阵来概括某篇文章)为基础,通过对图像所有的interest points用[harris affine detector]来
产生一个bag of keypoints 对图像进行描述。

不过一套训练数据里所有的keypoints的数量是相当大的，这里论文的另外一个看点就是用k-means对所有的keypoints进行归类，每个cluster之中保含类似的keypoints，而这时，每个图像里的keypoints 在每个cluster里的出现次数将会给统计并且生成一个bag of keypoints. 

通过naive bayes或svm 进行训练，在论文里分类的结果还不错.
有几个我觉得也许可以改进的地方:

>   1 在原论文里：每种图像生成的keypoints的数量是不同的，为了避免bias作者在clustering的时候在每类图像里随机选了5000个keypoints，我觉得如果选的时候可以把stop words的概念加进去，每个class都有的keypoint去除掉的话应该能增加discrimination.

>   2 在测试的时候我觉得如果一个keypoint离2个以上的cluster距离都差不多的话，应该可以把它当作IR里的‘生词’一样忽略掉.
感觉以上这两点应该能对算法有一个改进，以后有空得研究下。

还有在论文里作者在做测试的时候没有使用no-object的图像进行训练和测试，我觉得如果加进去的话，结果应该会差一个档次。

参考:
http://en.wikipedia.org/wiki/Bag_of_words_model_in_computer_vision.

这里是[作者介绍算法的视频],解释的相当不错，不过好像视频后半部分看不了。

[bag of words]:http://en.wikipedia.org/wiki/Bag_of_words_model
[harris affine detector]:http://en.wikipedia.org/wiki/Harris_affine_region_detector
[作者介绍算法的视频]:http://videolectures.net/lmcv04_dance_vcbk/
[Categorizing nine visual classes using local appearance descriptors]:http://www.xrce.xerox.com/index.php/content/download/16612/118527/file/willamowski.pdf
