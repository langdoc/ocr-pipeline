# IKDP project's OCR pipeline

This repository contains description of the OCR pipeline as used at the moment within Kone Foundation project "Language Documentation meets Language Technology: The Next Step in the Description of Komi". Besides Zyrian Komi materials, the pipeline has also bene used with Kildin Saami materials.

Our work has focused into those materials that are in Public Domain, are clearly licensed, or for which we have negotiated transparent rights for reuse. 

Specific aspect of our work has been that we have worked on text collections for which the original archived audio in many cases can be retrieved. We have not started to align audio and text systematically, since this would be basically endless manual work, and these resources could be better allocated into correction and checking the edited text and associated audio.

## OCR engines

### [Ocropy](https://github.com/tmbdev/ocropy)

Ocropy models start to work very fast, and are accurate, but the page segmentation doesn't seem to be as sophisticated as on Tesseract. It is not possible to run multiple languages at the same time like in Tesseract.

### [Tesseract](https://github.com/tesseract-ocr/tesseract)

We have been using [ocrd-train](https://github.com/OCR-D/ocrd-train) from [OCR-D project](https://ocr-d.github.io/) to build Tesseract models. The only problem has been that we haven't figured out how to best train Tesseract model from the scratch, which possibly would be the best approach in our situation. At the moment training a Tesseract model works well, once there are enough training lines. This makes it difficult to train a Tesseract model with minimal amount of training data, which works well on Ocropy.

### [Transkribus](https://transkribus.eu/)

Works well, and is at least at the moment free to use. Only available tool that is able to work with hand written text. New online user interface is very well developed, and seems suitable for collaborative work i.e. within teaching setting. The models trained on Transkribus tend to be extremely good and bootsrap very fast. The only minus is the lack of transparency in the training process, as the software used is not all open source. Access to the model training interface has to be requested from the developers.

## Pipelines

With Ocropy the training data can be created by starting with a folder full of wanted images. Ocropy will binarize and rename the images into their own folder. We have usually added new pages in batches and named these as `train_part_1`, `train_part_2` etc. This makes it easy to control what images went into which batch.

```
ocropus-nlbin original_images_1/*.png -o train_part_1
ocropus-gpageseg 'train_part_1/*.bin.png'
ocropus-gtedit html train_part_1/*/*.png -o train_part_1.html
```

This creates an HTML file that can be opened and edited in Firefox, displaying the lines and empty boxes for text. For the first batch manual typing is maybe the best alternative, or if the text is already available, then to copy it to correct segments.

The images can be written back to file structure so that they turn into Ground Truth text lines next to line images:

```
ocropus-gtedit extract -O train_part_1.html
```

A model can be trained with:

```
ocropus-rtrain -c ./train/*/*gt.txt -o una-01-58a2a7 -d 20 ./train_part_1/*/*png
```

Parameter `-c` tells Ocropy to find characters from the text files. Some collegues have reported better accuracy by specifying the character set manually, and this is worth testing.

**TODO:** Explanation on similar Tesseract workflow etc.

## OCR evaluation tools

- Eddie Antonio Santos's [ocreval](https://github.com/eddieantonio/ocreval)
- Ocropy's [ocropus-econf](https://github.com/tmbdev/ocropy)

## Conventions (**CLEAN OUT AND ADD SOON**)

- Ocropy training data to Tesseract training data script
- Structured text file to EAF script
- HOCR -> EAF script
- Transliteration patterns used
