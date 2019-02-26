# IKDP project's OCR pipeline

This repository contains description of the OCR pipeline as used at the moment within Kone Foundation project "Language Documentation meets Language Technology: The Next Step in the Description of Komi". Besides Zyrian Komi materials, the pipeline has also bene used with Kildin Saami materials.

Our work has focused into those materials that are in Public Domain, are clearly licensed, or for which we have negotiated transparent rights for reuse. 

Specific aspect of our work has been that we have worked on text collections for which the original archived audio in many cases can be retrieved. We have not started to align audio and text systematically, since this would be basically endless manual work, and these resources could be better allocated into correction and checking the edited text and associated audio.

## OCR tools

### Ocropy

Models start to work very fast, and are accurate, but the page segmentation doesn't seem to be as sophisticated as on Tesseract.

### Tesseract

We have been using [ocrd-train](https://github.com/OCR-D/ocrd-train) from [OCR-D project](https://ocr-d.github.io/) to build Tesseract models. The only problem has been that we haven't figured out how to best train Tesseract model from the scratch, which possibly would be the best approach in our situation. At the moment training a Tesseract model works well, once there are enough training lines. This makes it difficult to train a Tesseract model with minimal amount of training data, which works well on Ocropy.

### Transkribus

Works well, and is at least at the moment free to use. New online user interface is very well developed, and seems suitable for collaborative work i.e. within teaching setting. The models trained on Transkribus tend to be extremely good and bootsrap very fast. The only minus is the lack of transparency in the training process, as the software used is not all open source.

## Conventions (**CLEAN OUT AND ADD SOON**)

- Ocropy training data to Tesseract training data script
- Structured text file to EAF script
- HOCR -> EAF script
- Transliteration patterns used
