J. Hocking and M. Puttkammer, "Optical character recognition for South African languages," 2016 Pattern Recognition Association of South Africa and Robotics and Mechatronics International Conference (PRASA-RobMech), Stellenbosch, South Africa, 2016, pp. 1-5, doi: 10.1109/RoboMech.2016.7813139. keywords: {Engines;Optical character recognition software;Training;Character recognition;Feature extraction;Manuals;Adaptive optics;optical character recognition;OCR;South African languages},

M. K. Dauda, U. Musa and H. Al-Barhamtoshy, "Hausa Handwriting Character Recognition Using CNN and Tesseract," 2025 2nd International Conference on Advanced Innovations in Smart Cities (ICAISC), Jeddah, Saudi Arabia, 2025, pp. 1-6, doi: 10.1109/ICAISC64594.2025.10959458. keywords: {Handwriting recognition;Accuracy;Biological system modeling;Optical character recognition;Writing;Natural language processing;Fabrics;Character recognition;Convolutional neural networks;Cultural differences;Handwritten characters;Character recognition;Hausa language;African languages;Nigerian Languages},

https://mattrickard.com/fine-tuning-an-ocr-model

https://www.youtube.com/watch?v=SvhoBT-PnME

https://www.youtube.com/watch?v=KE4xEzFGSU8

Clone Github Tesstrain repo. https://github.com/tesseract-ocr/tesstrain#

Create a data folder inside it and move ocr-trainset into it.
Rename ocr-trainset to taa-ground-truth
Replace files, keeping same format, with .gt.txt file of taa language text, and image file.

Intent: due to low-resource availability, fine-tune english Tesseract LSTM to understand new characters.
https://github.com/tesseract-ocr/tesstrain/blob/eea5d7814ce2cac6f5ae660d51c8aa2caba41f10/README.md#provide-ground-truth-data

* Generate test data with full range of unichar code characters present in the dictionary.
* Use text to image function and match typefont of the PDF.
