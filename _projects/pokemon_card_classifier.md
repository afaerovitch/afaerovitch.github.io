---
layout: page
title: Pokemon Card Classifier
description: Building a computer vision pipeline to detect and classify Pokemon cards from marketplace images
img: /assets/img/pokemon_card_classifier/Thumbnail.png
importance: 1
category: School
featured: true
---

## Overview

For my final project in my machine learning course, I built a computer vision pipeline to identify and classify Pokemon cards from eBay listing images. I wanted to see whether a practical workflow could take noisy marketplace photos, isolate the card region, and still make a reliable prediction on the final card class. The project was inspired by Jack Baumgartel's MTG Card Recognition work, but adapted for Pokemon cards and my own dataset collection process.

<div class="row mt-3">
	<div class="col-sm mt-3 mt-md-0">
		{% include figure.liquid loading="eager" path="assets/img/pokemon_card_classifier/RegionBoundingBoxes.JPG" class="img-fluid rounded z-depth-1" %}
	</div>
</div>
<div class="caption">
	The YOLO11n detector found the card region so I could compare automatic bounding boxes against the hand-cropped version of the same image.
</div>

### Technology Stack

- **Language:** Python
- **Models:** YOLO11n for object detection, YOLOv8 for classification
- **Other Tools:** Web scraping, image preprocessing, data augmentation

## Pipeline

The process started with web scraping eBay listings for a set of 100 Pokemon cards that I chose to test on. From there, I used object detection bounding boxes from the YOLO11n model to crop the images and compare the automatically detected crops against my hand-cropped photos.

Once I had the cropped images, I introduced variance through rotation and color grading so the model would see a wider range of inputs during training. That step mattered because marketplace images are rarely clean or consistent, and I wanted the classifier to generalize beyond the exact examples I collected.

After preprocessing, I trained a YOLOv8 model to classify the cropped card images. The end result was a system that could take in raw listing photos, isolate the relevant region, and classify the card with strong accuracy.

<div class="row mt-3">
	<div class="col-sm mt-3 mt-md-0">
		{% include figure.liquid loading="eager" path="assets/img/pokemon_card_classifier/CroppedCardImages.JPG" class="img-fluid rounded z-depth-1" %}
	</div>
</div>
<div class="caption">
	Cropped card images after preprocessing and augmentation.
</div>

## Results & Performance

The final model reached **94.9% accuracy** with a **0.365 loss**. That gave me confidence that the pipeline was capturing the card region well enough for the classifier to work reliably, even when the original images were messy or inconsistent.

I also tracked the intermediate outputs from the detection and preprocessing stages so I could compare bounding-box crops, hand-cropped images, and the final classification results. The confusion matrix made it easier to see where the model was performing well and where the remaining errors clustered.

<div class="row mt-3">
	<div class="col-sm mt-3 mt-md-0">
		{% include figure.liquid loading="eager" path="assets/img/pokemon_card_classifier/Results.JPG" class="img-fluid rounded z-depth-1" %}
	</div>
</div>
<div class="caption">
	The final evaluation results summarized the model's performance on the test set.
</div>

## Future Improvements

- [ ] Expand the dataset beyond the initial 100 cards
- [ ] Add more image variety from different marketplaces and lighting conditions
- [ ] Improve detection and cropping for partially occluded cards
- [ ] Compare performance against additional classification architectures