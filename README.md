  # Big-Data-Africa-School-2026
## Projet 
<h3> Self-Explainable AI vs. Post-Hoc Explanations: Interpreting AI Decisions in Medical Image Classification. </h3>

## Abstract
Convolutional Neural Networks (CNNs) have been widely adopted across various sectors, including healthcare, due to their remarkable ability to solve complex medical imaging tasks, often surpassing human performance. However, despite their impressive potential for medical image classification, CNN-based systems are often considered “black boxes,” as their decision-making processes remain opaque to users. This lack of transparency poses a significant barrier to their adoption in clinical settings, where interpretability is essential.
Post-hoc explanation techniques, such as Grad-CAM and LIME, attempt to provide visual interpretations of AI decisions. However, these methods face several limitations, including inconsistency, unreliability, and sensitivity to small input perturbations. These flaws can result in differing explanations for similar inputs, ultimately undermining their trustworthiness and clinical applicability. Given the importance of transparency and interpretability in healthcare, there is a clear need for more robust and reliable explainability methods in AI-driven medical image analysis.
As an alternative, inherently interpretable models, often referred to as white-box or self-explainable models, have been proposed. These models aim to embed interpretability directly into their architecture. However, they can be more challenging to implement and train compared to widely used black-box models.
In this project, participants will train and evaluate white-box CNNs and compare their performance and interpretability to conventional black-box CNNs. Additionally, they will assess the quality of explanations provided by white-box models against popular post-hoc explanation techniques applied to their black-box counterparts, to determine which approach offers more reliable and clinically useful insights.

## Method
Leveraging the inherent localization properties of convolution operations, a recently proposed method enables black-box CNN models to become inherently interpretable [1]. This is achieved by removing the final global average pooling layer found in classical CNNs and replacing the fully connected classification layers with a convolutional class-evidence layer. This layer directly generates evidence maps from the feature maps at the penultimate layer.
Predictions are then obtained by averaging the values within each evidence map and passing the resulting values through a softmax function to produce a probability distribution. The explicit class-evidence layer can be viewed as a soft approximation of class activation maps (Soft-CAMs), generating transparent explanation maps that are directly integrated into the model’s prediction process. Furthermore, the quality of these explanations can be improved by applying a Lasso penalty to the class evidence, promoting either sparse or dense explanations depending on the specific task requirements.
In this project, participants will implement this technique to transform black-box CNNs into white-box models. They will then evaluate the interpretability of the resulting models using a range of explainable AI (XAI) metrics, including precision localization [2], sensitivity [3], activation precision[4], and activation sensitivity[1].

## Datasets
The primary dataset for this project is the publicly available RSNA Chest X-ray Dataset for pneumonia detection. This dataset is particularly suitable for evaluating model explanations, as it includes bounding box annotations for pneumonia cases. It contains 30,227 frontal-view chest radiographs categorized into three classes: “Normal,” “No Opacity/Not Normal,” and “Opacity” (indicative of pneumonia). For the purposes of this project, only the binary classification task—distinguishing between “Normal” and “Opacity”—will be considered, resulting in a subset of 14,863 images.

While the RSNA Chest X-ray Dataset will serve as the main focus, participants are also encouraged to explore the ISIC Challenge Datasets for skin disease classification. Some of these datasets provide segmentation masks, offering additional opportunities to evaluate and compare model interpretability in different medical imaging contexts.

## Evaluation metrics
For the classification task, standard performance metrics such as Accuracy and Area Under the ROC Curve (AUC) will be used.
To evaluate the quality of explanations, the following metrics may be employed:
- __Precision Localization__ [2]: This metric requires ground truth annotations or segmentation masks. It measures the proportion of positively activated regions in the explanation map that overlap with the annotated ground truth, indicating how well the explanation aligns with clinically relevant regions.
- __Activation Precision__ [4]: Also relying on ground truth masks, this metric calculates the proportion of the model’s positive activations that fall within the annotated region. It extends precision localization to better handle tasks where the region of interest spans a large area of the image.
- __Activation Sensitivity__ [1]: A variation of activation precision, this metric additionally penalizes false negatives, i.e., areas within the ground truth region that are not highlighted by the explanation, thereby rewarding comprehensive coverage of the disease-relevant area.
- __Sensitivity (Faithfulness Metric)__ [3] This metric does not require ground truth annotations. It assesses the faithfulness of the explanation by iteratively masking the most informative regions (as indicated by the explanation map) and observing the resulting drop in the model's prediction confidence. A larger drop implies greater faithfulness of the explanation.

## Tasks
The primary task involves training both black-box models and their corresponding white-box counterparts, then evaluating their classification performance and the quality of their explanations. For the white-box models, participants will experiment with different regularization values to identify the optimal trade-off between predictive accuracy and interpretability.

## Supporting materials
- An initial [GitHub](https://anonymous.4open.science/r/SoftCAM-E1A3/README.md) repository will be provided, built with PyTorch, containing code for training both black-box and corresponding white-box models. The implementation of the explainability metrics will also be included.
- Post-hoc explanations for black-box models will be generated using existing XAI libraries such as Captum or TorchCAM, while explanations for white-box models will be produced directly alongside the model’s predictions.

## References
[1] Djoumessi, K., & Berens, P. (2025, May 23). Soft-CAM: Making black box models self-explainable for high-stakes decisions. arXiv.org. https://arxiv.org/abs/2505.17748
[2] Djoumessi, K, Ilanchezian, I., Kühlewein, L., Faber, H., Baumgartner, C. F., Bah, B., Berens, P., & Koch, L. M. (n.d.). Sparse activations for interpretable disease grading. OpenReview. https://openreview.net/forum?id=us8BFTsWOq
[3] Yeh, C., Hsieh, C., Suggala, A. S., Inouye, D., I., & Ravikumar, P. (2019, January 27). On the (In) fidelity and Sensitivity for Explanations. arXiv.org. https://arxiv.org/abs/1901.09392
[4] Barnett, A. J., Schwartz, F. R., Tao, C., Chen, C., Ren, Y., Lo, J. Y., & Rudin, C. (2021). A case-based interpretable deep learning model for classification of mass lesions in digital mammography. Nature Machine Intelligence, 3(12), 1061–1070. https://doi.org/10.1038/s42256-021-00423-x
