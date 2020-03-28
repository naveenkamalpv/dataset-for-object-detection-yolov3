<h1> Dataset for object_detection </h1>


# 1.0 Getting Started

## 1.1 Installation

Python3 is required.

1. Clone this repository
   ```bash
   git clone https://github.com/naveenkamalpv/dataset-for-object_detection-yolov3-
   ```
2. Install the required packages
   ```bash
   pip3 install -r requirements.txt
   ```
Peek inside the requirements file if you have everything already installed. Most of the dependencies are common libraries.

## 1.2 Launch the ToolKit to check the available options
First of all, if you simply want a quick reminder of al the possible options given by the script, you can simply launch, from your console of choice, the [main.py](main.py). Remember to point always at the main directory of the project
   ```bash
   python3 main.py
   ```
or in the following way to get more information
   ```bash
   python3 main.py -h
   ```

# 2.0 Use the ToolKit to download images for Object Detection
The ToolKit permit the download of your dataset in the folder you want (`Dataset`as default). The folder can be imposed with the argument
`--Dataset` so you can make different dataset with different options inside.

As previously mentioned, there are different available options that can be exploited. Let's see some of them.

## 2.1 Download different classes in separated folders
Firstly, the ToolKit can be used to download classes in separated folders. The argument `--classes` accepts a list of classes or
the path to the file.txt (`--classes path/to/file.txt`) that contains the list of all classes one for each lines (classes.txt uploaded as example).

**Note**: for classes that are composed by different
words please use the `_` character instead of the space (only for the inline use of the argument `--classes`).
Example: `Polar_bear`.

Let's for example download Apples and Oranges from the validation set. In this case we have to use the following command.
  ```bash
   python3 main.py downloader --classes Apple Orange --type_csv validation
   ```
The algorith will take care to download all the necessary files and build the directory structure like this:

```
main_folder
│   main.py
│
└───OID
    │   file011.txt
    │   file012.txt
    │
    └───csv_folder
    |    │   class-descriptions-boxable.csv
    |    │   validation-annotations-bbox.csv
    |
    └───Dataset
        |
        └─── test
        |
        └─── train
        |
        └─── validation
             |
             └───Apple
             |     |
             |     |0fdea8a716155a8e.jpg
             |     |2fe4f21e409f0a56.jpg
             |     |...
             |     └───Labels
             |            |
             |            |0fdea8a716155a8e.txt
             |            |2fe4f21e409f0a56.txt
             |            |...
             |
             └───Orange
                   |
                   |0b6f22bf3b586889.jpg
                   |0baea327f06f8afb.jpg
                   |...
                   └───Labels
                          |
                          |0b6f22bf3b586889.txt
                          |0baea327f06f8afb.txt
                          |...
```

## 2.2 Download multiple classes in a common folder
This option allows to download more classes, but in a common folder. Also the related notations are mixed together with
 the already explained format (the first element is always the name of the single class). In this way, with a simple
 dictionary it's easy to parse the generated label to get the desired format.

Again if we want to download Apple and Oranges, but in a common folder
  ```bash
   python3 main.py downloader --classes Apple Orange --type_csv validation --multiclasses 1
   ```

# 3.0 Download images from Image-Level Labels Dataset for Image Classifiction
The Toolkit is now able to acess also to the huge dataset without bounding boxes. This dataset is formed by 19,995 classes and it's already divided into train, validation and test. The command used for the download from this dataset is ```downloader_ill``` (Downloader of Image-Level Labels) and requires the argument ```--sub```. This argument selects the sub-dataset between human-verified labels ```h``` (5,655,108 images) and machine-generated labels ```m``` (8,853,429 images). An example of command is:
```bash
python3 main.py downloader_ill --sub m --classes Orange --type_csv train --limit 30
```
