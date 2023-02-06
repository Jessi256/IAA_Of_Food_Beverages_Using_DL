# Image aesthetics assessment (IAA) of food and beverages using deep learning

To support the research and applications that are related to image aesthetics assessment (IAA) of food and beverages, the main contributions of this repository are two-fold:

<ul>
  <li>Introduction of the brand-new dataset for food and beverage images RIAA.</li>
  <li>A systematic evaluation of how far a deep learning system can be used to learn the aesthetics of food and beverage images that reflect the taste of laypersons or experts in the field. Therefore, several test cases on RIAA are defined along the typical flow for IAA. These test cases are conducted using simple baseline models that are competitive with the current state-of-the-art models.</li>
</ul>

***
<h2>Background</h2>

In recent years, a rapid growth of digital presentation and manipulation of food and beverages in online content has occurred [1–4]. This is due to growing interest in “foodporn” and “gastroporn” [5] as well as a growing attention in the visual presentation of products by marketers and advertisers [1, 6, 7]. According to statistics from the rise of Instagram, almost 85 percent of the images on its social media site are related to food [8]. Additionally, there are more than 853 million images associated with the hashtags “food”, “beverage”, “foodporn”, and “foodblogger” [9]. Consequently, identifying aesthetic food and beverage images is an important visual analysis task for social media and ranking systems that are related to food. The image aesthetics assessment (IAA) aims to distinguish aesthetic, high-quality images from unaesthetic, low-quality ones with the use of binary classification or scoring. Nevertheless, IAA of food and beverage images remains a challenging and relatively unexplored area in terms of deep learning. This is due to the lack of food and beverage image datasets and practical experience [10].

***
<h2>RIAA: Recipe Image Aesthetics Assessment</h2>
RIAA is a brand-new, self-created and large-scale dataset for aesthetics assessment of food and beverage images. Compared to the existing food and beverage aesthetics dataset <a href="https://github.com/Openning07/GPA">GPD </a>, this dataset has a more diverse label annotation process, including annotations made from over 100 laypersons. This ensures a more diverse representation of labels and eliminates the bias that can come from a single annotator. 20,800 food and beverage images are collected with layperson-annotated labels (i.e., aesthetically positive, neutral, or negative) to build this dataset.
<img src="https://github.com/Jessi256/IAA_Of_Food_Beverages_Using_DL/blob/main/Images/RIAA%20Dataset%20Examples.png" alt="RIAA Dataset examples">



***

<h2>Experimental Study</h2>
To ensure reliable results and a systematic evaluation for the reaserch question “Can a deep learning system learn aesthetics of food and beverage images that reflect the taste of a layperson/expert in the field?” several state-of-the-art test cases on RIAA are conducted along the typical flow for IAA. The three test cases label preprocessing, image preprocessing and modeling are constructed using the "ceteris paribus" principle. The "ceteris paribus" approach allows the influences of one variable to be isolated from the influences of other variables, so the effects of each variable can be measured independently. A red setting symbol indicates the variable that is changing within the test case, while all other variables remain the same. This approach can help identify which variables have the most significant impact on the model’s accuracy.

<img src="https://github.com/Jessi256/IAA_Of_Food_Beverages_Using_DL/blob/main/Images/Methodology.png" alt="Methodology">

For each test case a performance evaluation is conducted using percentage accuracy (A) and balanced accuracy (BA) as metrics. This evaluation helps to explore the possibilities of IAA on food and beverage images considering different influencing factors. Compared to accuracy, balanced accuracy is a metric that considers both false positives and false negatives and provides a more comprehensive measure of model performance. It is useful for datasets with an uneven class distribution as it takes the imbalance in the data into account.

<h3>1. Label Preprocessing</h3>
<img src="https://github.com/Jessi256/IAA_Of_Food_Beverages_Using_DL/blob/main/Images/Label_Preprocessing.PNG" alt="Label Preprocessing">

<h3>2. Image Preprocessing</h3>
<img src="https://github.com/Jessi256/IAA_Of_Food_Beverages_Using_DL/blob/main/Images/Image_Preprocessing.PNG" alt="Image Preprocessing">

<h3>3. Modeling</h3>
<img src="https://github.com/Jessi256/IAA_Of_Food_Beverages_Using_DL/blob/main/Images/Modeling.PNG" alt="Modeling">

<h3>4. Further Investigations</h3>
<img src="https://github.com/Jessi256/IAA_Of_Food_Beverages_Using_DL/blob/main/Images/Further_Investigations.PNG" alt="Further Investigations">

<h3>Summary</h3>
First, three label preprocessing approaches are tested with VGG16 on the RIAA dataset from scratch. To begin with, VGG16 is trained on an imbalanced dataset, then on a balanced dataset, and finally, a weighted VGG16 is trained on the imbalanced dataset. VGG16- Dweighted, unbalanced yields better performing than unweighted VGG16- Dunbalanced or VGG16- Dbalanced. Additionally, VGG16- Dweighted, unbalanced achieves better balanced accuracy prediction of aesthetic and unaesthetic images.
Second, four image preprocessing approaches warping Iwarped, cropping Icropped, padding Ipadded and random data augmentation Iaugmentation are implemented with VGG16 from scratch to see whether data augmentation distorts the image aesthetics information and impairs the performance of the IAA model. Interestingly, there is no significant difference in model performance between warped and center-cropped food and beverage input images for IAA. VGG16- Icropped slightly outperforms VGG16- Iwarped. VGG16- Ipadded does not perform very well and suffers from overfitting. By randomly augmenting image inputs, VGG16- Iaugmentation suffers significantly in training as well as in testing. These results show that random data augmentation distorts the image information and impairs the performance of the model. Considering the test results, the question arises to what extent the image ratio and editing influences the aesthetics of food and beverage images. For different image ratios no significant aesthetic differences are predicted by VGG16- Iwarped. Consequently, cropping is a minor aspect of the aesthetics of food and beverage images. Edited images (such as warm colors vs. cold colors, low sharpness vs. high sharpness, etc.) demonstrate that VGG16- Iwarped can reflect both deterioration and improvement in the image's aesthetics. According to the results, the model could be used in the future to give laypersons a recommendation for image optimization. <br> 
<br> 
Third, the modeling test case is subdivided into two parts: training from scratch with vanilla CNNs and fine-tuned CNNs with regularization strategy. For training from scratch the vanilla state-of-the-art CNNs VGG-16, ResNet50, Inception-v3 and Xception base models are initialized. For fine-tuning the same models are pretrained on ImageNet. After training the models for 10 epochs, the convolutional base (first 80 percent of the base model) is frozen. To avoid overfitting, dropout-layers (0.2) are implemented in the classifier head of each pretrained model for regularization strategy. Overall, the vanilla base models from scratch VGG16vanilla, ResNet50vanilla, Inception-v3vanilla and Xceptionvanilla are suitable for IAA of food and beverage images. ResNet50vanilla performs best with an overall accuracy above 80 percent. Inception-v3vanilla has the highest balanced accuracy at 79.06 percent. Based on the GPD dataset, Xceptionvanilla performs best in the generalization test with 69.42 percent. In the overall evaluation, vanilla models yield better results on the RIAA dataset than fine-tuned models. However, the fine-tuned models achieve enhanced generalization ability on GPD and Inception-v3fine-tuned even outperforms the generalization test from [10]. False positive examples show an image trend with low brightness, little color contrast, and dark or restless backgrounds, whereas false negative examples show an image trend with high brightness, color contrast, harmonic colors, and uniform (and uncluttered) backgrounds. Moreover, most false positive examples include food with a higher energy density. <br> 
<br> 
To reduce cultural bias, the fine-tuned CNNs are trained in further investigation again on a merged RIAA and GPD dataset. As a result, model performance is greatly improved, particularly for Inception-v3fine-tuned and Xceptionfine-tuned. Overall, Inception-v3fine-tuned is the most appropriate model, which performs the highest on both the GPD and the GPD + RIAA training and test data. With 85.17 percent accuracy on GPD + RIAA test data, Inception-v3fine-tuned is comparable to state-of-the-art models in IAA. <br> 
<br> 
Summarizing, it can be concluded that a deep learning system can learn aesthetics of food and beverage images that reflect the taste of a layperson/experts to a certain level. Nevertheless, this task remains challenging due to many factors relating to the aesthetics of food and beverage images, such as preprocessing steps for deep learning, photographic effects, cultural influences, individual tastes, and food-dense stimuli. 

***
<h2>References</h2>
<p>[1]	C. Spence, K. Motoki, and O. Petit, “Factors influencing the visual deliciousness / eye-appeal of food,” Food Quality and Preference, vol. 102, p. 104672, 2022, doi: 10.1016/j.foodqual.2022.104672.</p>
<p>[2]	S. Coary and M. Poor, “How consumer-generated images shape important consumption outcomes in the food domain,” Journal of Consumer Marketing, vol. 33, no. 1, pp. 1–8, 2016, doi: 10.1108/JCM-02-2015-1337.</p>
<p>[3]	S. Zhang et al., “Tasting More Than Just Food: Effect of Aesthetic Appeal of Plate Patterns on Food Perception,” Foods (Basel, Switzerland), vol. 11, no. 7, 2022, doi: 10.3390/foods11070931.</p>
<p>[4]	C. Velasco, F. Barbosa Escobar, O. Petit, and Q. J. Wang, “Impossible (Food) Experiences in Extended Reality,” Front. Comput. Sci., vol. 3, 2021, doi: 10.3389/fcomp.2021.716846.</p>
<p>[5]	E. M. Mcdonnell, Food Porn: The Conspicuous Consumption of Food in the Age of Digital Reproduction: The Edible Image. London: Palgrave Macmillan, 2016.
<p>[6]	L. N. van der Laan, D. T. D. de Ridder, M. A. Viergever, and P. A. M. Smeets, “Appearance matters: neural correlates of food choice and packaging aesthetics,” PloS one, vol. 7, no. 7, 1-11, 2012, doi: 10.1371/journal.pone.0041738.</p>
<p>[7]	M. Vukmirovic, “The effects of food advertising on food-related behaviours and perceptions in adults: A review,” Food research international (Ottawa, Ont.), vol. 75, pp. 13–19, 2015, doi: 10.1016/j.foodres.2015.05.011.</p>
<p>[8]	C. Holmberg, J. E Chaplin, T. Hillman, and C. Berg, “Adolescents' presentation of food in social media: An explorative study,” Appetite, vol. 99, pp. 121–129, 2016, doi: 10.1016/j.appet.2016.01.009.</p>
<p>[9]	Contributions of #food on Instagram. [Online]. Available: https://www.instagram.com/ (accessed: Dec. 29 2022).</p>
<p>[10]	K. Sheng et al., “Learning to assess visual aesthetics of food images,” Comp. Visual Media, vol. 7, no. 1, pp. 139–152, 2021a, doi: 10.1007/s41095-020-0193-5.</p>
 
