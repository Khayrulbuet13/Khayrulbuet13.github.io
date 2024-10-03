---
title: "Lymphocyte Cell Classification using Knowledge Distillation and Transfer Learning" 
date: 2024-01-01
status: "Ongoing"
tags: ["Knowledge Distillation", "Transfer Learning", "Cell Classification", "FPGA"]
author: ["Khayrul Islam"]
description: "Developing an efficient model for lymphocyte cell classification using Knowledge Distillation and Transfer Learning, with real-time deployment on FPGA for T-cell detection." 
summary: "Building a scalable cell classification model for T4 vs B cell and T8 vs B cell, leveraging Knowledge Distillation for speed optimization and Transfer Learning for zero-shot inference capabilities. The final deployment is planned for FPGA to enable real-time T-cell detection."
cover:
    image: "project4.png"
    alt: "Lymphocyte Cell Classification"
    relative: false
editPost:
    URL: "https://github.com/Khayrulbuet13/LymphoMNIST"
    Text: "GitHub Repository"
role: "Lead Developer"

---

##### Project Status:

- **Status**: Ongoing
- **Start Date**: 2024-01-01
- **End Date**: Not applicable yet

---

##### Overview:

<div class="justify-text">

In this project, we present a cutting-edge approach to lymphocyte cell classification using Knowledge Distillation (KD) and Transfer Learning techniques. Our dataset comprises 80,000 images, supporting the training and validation of cell classification models. After installing our pip-installable package, users can seamlessly download and use the dataset. 

We focus on optimizing a larger teacher model for T4 vs B cell classifications and training a smaller student model that achieves approximately double the inference speed and requires about 50% less computational resources. Furthermore, we demonstrate the capability of Transfer Learning for T8 vs B cell classifications, allowing the model to perform zero-shot inference and be fine-tuned for other lymphocyte cell types. 

The project also involves deploying the model on an FPGA platform to achieve real-time T-cell detection, advancing the potential for real-time biomedical applications.

</div>



---

##### Key Responsibilities / Contributions:

- **Lead Developer**: I am responsible for developing the KD models and Transfer Learning techniques to improve both speed and accuracy in cell classification.
- Managed the creation of a pip-installable package that simplifies access to the dataset and models.
- Designed and implemented the smaller student model for inference speed optimization and computational resource reduction.
- Demonstrated the model’s transfer learning capabilities for zero-shot inference of other lymphocyte cell types.
- Leading the deployment efforts of the model on FPGA to enable real-time detection of T cells in biomedical applications.

---

##### Tools & Technologies:

- **Languages**: Python, C++
- **Frameworks**: PyTorch, TensorFlow
- **Other Tools**: FPGA, Git, Docker

---

##### Current Progress:

<div class="justify-text">

The project is in the development phase, focusing on model training and optimization. The pip-installable package is functional, allowing seamless access to the dataset. The teacher and student models have been tuned for optimal performance, and transfer learning results for T8 vs B cell classifications have been promising. FPGA deployment is the next major milestone.

</div>



- **Milestones**: Dataset and models developed; Transfer learning demonstrated.
- **Current Focus**: FPGA deployment for real-time cell detection.

<!-- --- -->

<!-- ##### Figures / Diagrams (Optional): -->

<!-- - Figure X: A visual representation of the KD-based model architecture used for cell classification.

![Cell Classification](cell_classification.png) -->

---

##### Roadmap / Next Steps (For Ongoing Projects):

- Finalize FPGA deployment for real-time T-cell detection.
- Further tune the model for zero-shot inference on additional lymphocyte cell types.
- Test the models in biomedical labs to validate real-world applicability.

<!-- --- -->

<!-- ##### Related Materials:

- [Project Code](https://github.com/project_repo)
- [Documentation](https://project-docs-url.com)
- [Presentation Slides](presentation.pdf)
![alt text](image.png) -->