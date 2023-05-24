# Data Analysis

During the operation in the ELISSA laboratory or the simulation, the topic data can be recorded using [ROS bag](ros_bag). This data can be converted to csv files which usually are plotted with python. This process is described by an example on this page.

---
Table of Content:
- [Data Analysis](#data-analysis)
  - [Data Conversion](#data-conversion)
  - [Data Visualization](#data-visualization)
    - [Dependencies](#dependencies)
    - [Loading the Data](#loading-the-data)
    - [Processing the Data](#processing-the-data)

---

## Data Conversion

tbd

## Data Visualization

### Dependencies

The following packages are needed and imported first:

```python
import pandas as pd
from datetime import datetime, timedelta
from scipy.spatial.transform import Rotation
import matplotlib.pyplot as plt
import os
```

### Loading the Data

**Work in Progress**

To visualize the data, a python class is created. As an input, it receives the foldername containing the csv files. It is checked, that the folder exists. This ist happening in the `__init__` method:

```python
class Data:

    def __init__(self, foldername, delta_min=0.15, delta_max=2, convert_time_man=True, show_plots=False, save_plots=True):

        print(f'Reading data from folder {foldername}')

        # Get the data of the force sensors
        self.force_files = []
        self.force_files.append(f'{foldername}/__force_sens_00__dock_force.csv')
        self.force_files.append(f'{foldername}/__force_sens_01__dock_force.csv')
        self.force_files.append(f'{foldername}/__force_sens_02__dock_force.csv')
        self.force_files.append(f'{foldername}/__force_sens_03__dock_force.csv')

        # Get the data for the ff states
        self.state_files = []
        self.state_files.append(f'{foldername}/chaser__state.csv')
        self.state_files.append(f'{foldername}/chaser__state_goal.csv')
        self.state_files.append(f'{foldername}/target__state.csv')
```

The data is read from the csv file using the pandas package. The data is saved in easy to handle `dataframes`. These `dataframes` are saved in a list. During the loading, the separator must be specified. 

```python
 # Read the data from the csv files
        self.force_data = []
        self.force_data_raw = []
        for file in self.force_files:
            self.force_data.append(pd.read_csv(file, sep=','))
            self.force_data_raw.append(pd.read_csv(file, sep=','))
        self.state_data = []
        for file in self.state_files:
            self.state_data.append(pd.read_csv(file, sep=','))
```

### Processing the Data

Next, the loaded data is processed. Multiple steps are necessary, to put the available data in a efficiently usable format. First, the timestamps are converted to a `datetime` format for easier handling:

```python
# Convert the time into the datetime format
        for i, element in enumerate(self.force_data):
            tmp_list = []
            for time in self.force_data[i]['Timestamp']:
                tmp_list.append(datetime.fromtimestamp(time))
            self.force_data[i]['Timestamp'] = tmp_list
        for i, element in enumerate(self.state_data):
            tmp_list = []
            for time in self.state_data[i]['Timestamp']:
                tmp_list.append(datetime.fromtimestamp(time))
            self.state_data[i]['Timestamp'] = tmp_list
```

To get better structured data, the columns must be renamed. As at the end all data should be merged in one `dataframe`, we must ensure that no columns have the same name.

```python
        # Rename and sort the columns
        if plot_x or plot_vel:
            self.data[0] = self.clean_state(self.data[0], app='Goal_')
            self.data[1] = self.clean_state(self.data[1])
        if plot_wrench:
            self.data[2] = self.clean_wrench(self.data[2], app='Exc_')
        if plot_ctl_wrench:
            self.data[3] = self.clean_wrench(self.data[3], app='Ctl_')
        self.data[4] = self.clean_veh_state(self.data[4])
```


