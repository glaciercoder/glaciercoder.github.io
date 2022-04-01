---
layout: default
title:  "Simulink-Carsim combined simulation"
date:   2021-11-17 15:17:36 +0800
categories: control

---

 Collected documents and some basic usage for Carsim. 

​																																														——*Bingchuan Wei*

# Carsim Background

Carsim official Sites:https://www.carsim.com/products/carsim/index.php

Carsim quick start guide: https://www.carsim.com/downloads/pdf/CarSim_Introduction.pdf

An introduction to Carsim(**Highly recommended**!) or CarSim_quick_Start under `Help` folder: https://zhuanlan.zhihu.com/p/105850102

Official Video: https://www.bilibili.com/video/av59626289/

There are two main resources for carsim user help: one is official documents, the other is some domestic sites such as CSDN or ZhiHu. It's intriguing for me to find that google provides few such documents.

## Some key concepts and Ideas:

- Datasets: datasets store the data for car models and provide information for simulation
- Library: a library is a set of datasets organized in a unified UI layout, CarSim Run Control is most used library, we can change car models(datasets) under this library.
- Database: database contains a set of needed datasets and some examples,  it is recommended to have several databases to organize work. 
- VS: Vehicle Simulation,  casim defult interface is VS interface
- ADAS/AVs: Advanced Driving Assistance Systems/autonomous vehicles , used to simulation the traffic.
- VS Visualizer: component that makes the animation and draw simlulation results.
- CPAR file:  The “**Consolidated Parsfile**” is a file type that CarSim can create to transfer data between databases or users. CPAR  (file type extension .cpar) contains everything included in an expanded parsfile plus embedded copies of other linked files (primarily animator shapes and audio files). 
- Overlay: draw simulation results for different car models in one graph and make comparisons.
- System-Level modeling: carsim uses models of system level, rather than its accurate mechanical parameters for each components. These system-level parameters mainly comes from measuring.



## Carsim file structre

Sometimes our software doesn't respond to GUI operations so we need to manully operate some files. There are two important directories for Carsim

1. Installation directories(C:\Program Files (x86)\CarSimxxx_Prog)(xxx for version number)

   <img src="2021-11-17-simulink_carsim_combined_simulation.assets/Screen Shot 2021-11-19 at 1.50.03 PM.png" alt="Screen Shot 2021-11-19 at 1.50.03 PM" style="zoom:33%;" />

   - Help -> A comprehensive documents library (GUI->help will open this folder, but I can't)
   - Programs-> Solvers, an especially important folder
   - Resources: some display resources such as pictures and also some dll files. CPAR are in this folder which are used to create new database.
   - SGUI_LIB -> files needed for GUI

2. Library directories (C:\Users\Public\Document\Carsim2019.1_Data)

​		<img src="2021-11-17-simulink_carsim_combined_simulation.assets/Screen Shot 2021-11-19 at 1.55.06 PM.png" alt="Screen Shot 2021-11-19 at 1.55.06 PM" style="zoom:25%;" />

Literally, `library` folder contains library files, for example: vehicles, models, etc.

### Libraries, datasets and categories

Every library has its datasets. However, libraries are not parallel. For instance, *CarSim Run Control* contains *Vehicle assembly* and many other stuff, what if I create a dataset under Vehicle assembly? By experiments we can find that these created datasets will also appear under the top library: CarSim Run Control. The reason for this is that libraries are actually hierarchical. A dataset from a higher library is actually **linked** with dataset from lower library. More often than not, we want to modify the file from the current state. There are two ways to accomplish it:

1. **File->New Dataset Plus All Linked Datasets ** and **Drop Down Menu->Copy and Link**, these two methods will create two categories and put the new file into these new categories.
2. **Duplicate** : this will create a new dataset with a new title in the current category.



# Carsim WorkFlow

Here is a basic carsim workflow :

1. New a database (**File->New database from a consolidated parsfile**)	

A CPAR is actually a category, which contains some initial datasets, after creation, the navigation bar will display: 

[Database]Library;{category}Datasets, for example:

<img src="2021-11-17-simulink_carsim_combined_simulation.assets/Screen Shot 2021-11-19 at 5.50.17 PM.png" alt="Screen Shot 2021-11-19 at 5.50.17 PM" style="zoom:80%;" />

Our modification contains 

-  change of datasets: By **Duplicate**, we can create different datasets from a common points. They are under the same category. By **File->New Datasets plus all linked Datasets **, creat new datasets, typically used for changing car model. Tab **Datasets** can change between different datasets.

# Carsim simulink combined simulation

To use external controller, this file shows what carsim can do: https://www.carsim.com/downloads/pdf/CarSim_Math_Models.pdf

Official documents for combined simulation: https://www.carsim.com/products/supporting/simulink/index.php

A workflow example: https://www.carsim.com/downloads/pdf/Simulink_ABS_Example.pdf

Actually, the official video is totally rubbish, there are several points here:

1. 





Step:

1. launch carsim in simulink.







# Issues

1. After creating .slx file and choose models, the button **Send to simulink** is not activated.

2. Help button no response.

   Solved: Installed Acrobat Reader is broken and Carsim only uses this software, go drectly to the Help folder will solve this problem.
   
3. Video button not activated

​		Solved: First unlock the project, than run math model

4. Can not find S Function

​		A solution(may not work): https://cloud.tencent.com/developer/news/388100



# More 

An introduction http://www.360doc.com/content/20/1209/13/72814757_950375263.shtml

More on S Function: https://blog.csdn.net/acelit/article/details/59082349

More on car parameters design: https://blog.csdn.net/ERTFYANG/article/details/79872525

、