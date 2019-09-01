# Description of the Config.ini

The config.ini file contains the information for the alignment and ROIs to process the image. It consists of 3 main segments, which are described in the following sections:

* `[alignment]`
* `[Analog_Counter]`
* `[Digital_Counter]`


## Alignment

#### Main section [aligment]
In the main sections the parameter for the rotation is stored:


| Parameter        | Meaning           | Example        |
| ------------- | ------------- | ------------- |
| initial_rotation_angle | Fixed rotation angle for prealigment | `initial_rotation_angle=0` |

#### Sub section for reference [alignment.ref0],[alignment.ref1], [alignment.ref2]

Here the details for the fine alignment references are stored. There need to be 3 subsections ([alignment.ref0], [alignment.ref1], [alignment.ref2]) to ensure the affine transformation:

| Parameter        | Meaning           | Example        |
| ------------- | ------------- | ------------- |
| image | link and name of reference picture | `image=./reference/Ref_ZR.jpg` |
| pos_x | x target coordinate (upper left corner) | `pos_x=70` |
| pos_y | y target coordinate (upper left corner) | `pos_y=203` |


## Definition of ROIs
The ROIs are defined in two steps:
1. name - main section
2. details on position - sub section

For further processing there are two types of ROIs distinguished: 

* Analog_Counter: ROIs for analog counters
* Digital_Digit: ROIs for digital digits for OCR

The syntax of the parameters is identically for both categories.

#### Main sectin ROIs [Digital_Digit], [Analog_Counter]

Here a list of the ROIs is defined. The number is not limited. For each ROI a line with 'name[]' needs to be added. Don't forget the bracket [] also for only one single ROI.

| Parameter        | Meaning           | Example        |
| ------------- | ------------- | ------------- |
| names | naming of the ROIs and references to sub section | `name=ziffer1, ziffer2, ziffer3` |
| Modelfile | path to the Modelfile for the neural network | `Modelfile=./config/neuralnets/Train_CNN_Digital-Readout_Version2.h5` |
| LogImageLocation | path to storage of detected images for debugging / data collection. If this is empty, no logging will happen | `LogImageLocation=./log/digital_digit` |
| LogNames | name of dedicated ROIs to be stored. If this is disabled, all ROIs will be logged (if enabled) | `LogNames=zeiger3, zeiger4` |


#### Sub section of individual ROIs [Digital_Digits.name], [Analog_Counter.name]

The naming of the sub section depends on the ROI naming defined in the main section. For every ROI "xyz" defined in the main section there needs to be either a corresponding sub section (e.g. [Digital_Digits.xyz] with the following content:

| Parameter        | Meaning           | Example        |
| ------------- | ------------- | ------------- |
| pos_x | x coordinate ROI (upper left corner) | `pos_x=546` |
| pos_y | y coordinate ROI (upper left corner) | `pos_y=303` |
| dx | x lenght of the ROI | `dx=142` |
| dy | y length of the ROI | `dy=142` |


# Remark

**Currently there is no error handling implemented in the processing of the code. Therefore a carefull review of the ini file is substantial!**

## Example

~~~~
[alignment]
initial_rotation_angle=0

[alignment.ref0]
image=./config/Ref_ZR.jpg
pos_x=70
pos_y=203

[alignment.ref1]
image=./config/Ref_m3.jpg
pos_x=575
pos_y=79

[alignment.ref2]
image=./config/Ref_x0.jpg
pos_x=308
pos_y=406

[Digital_Digit]
names=ziffer1, ziffer2, ziffer3, ziffer4, ziffer5
Modelfile=./config/neuralnets/Train_CNN_Digital-Readout_Version2.h5
LogImageLocation=./log/digital_digit
#LogNames=zeiger3, zeiger4

[Analog_Counter]
names=zeiger1, zeiger2, zeiger3, zeiger4
Modelfile=./config/neuralnets/Train_CNN_Analog-Readout_Version2.h5
LogImageLocation=./log/analog_counter
#LogNames=zeiger3, zeiger4

[Analog_Counter.zeiger1]
pos_x=546
pos_y=303
dx=142
dy=142

[Analog_Counter.zeiger2]
pos_x=448
pos_y=416
dx=142
dy=142

[Analog_Counter.zeiger3]
pos_x=306
pos_y=451
dx=142
dy=142

[Analog_Counter.zeiger4]
pos_x=134
pos_y=366
dx=142
dy=142

    
[Digital_Digit.ziffer1]
pos_x=202
pos_y=49
dx=55
dy=90

[Digital_Digit.ziffer2]
pos_x=272
pos_y=49
dx=55
dy=90

[Digital_Digit.ziffer3]
pos_x=346
pos_y=49
dx=55
dy=90

[Digital_Digit.ziffer4]
pos_x=417
pos_y=49
dx=55
dy=90

[Digital_Digit.ziffer5]
pos_x=487
pos_y=49
dx=55
dy=90

~~~~

