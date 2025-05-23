# RadeonMaster

> [!NOTE]
> This module is only developed for Linux system!

RadeonMaster is a Python module for retrieving utilization and other information about Radeon GPUs. It is designed to work on Linux systems and relies on lm-sensors and radeontop for data collection.

## Features

- Retrieve Radeon GPU utilization
- Obtain additional information about the GPU

## Data Provided by RadeonMaster

- Event Engine
- GPU name
- GPU temp
- GPU type
- GPU usage
- GTT
- GTT PERCENTAGE
- GTT Total
- GTT Used
- Memory Clock
- Memory Clock PERCENT
- Memory Clock PERCENTAGE
- Memory Clock Total
- Memory Clock Used
- Primitive Assembly
- Sequencer Instruction Cache
- Shader Clock
- Shader Clock PERCENTAGE
- Shader Clock Total
- Shader Clock Used
- Shader Interpolator
- Texture Addresser
- VRAM
- VRAM PERCENTAGE
- VRAM Total
- VRAM Used
- Vertex Grouper + Tesselator
- bus address
- color block
- depth block
- scan converter

## Installation

 - ### Dependencies
    RadeonMaster requires lm-sensors and radeontop to be installed on your system. If you don't have them installed, you can   install them using your package manager:
  
    ```bash
    # For Debian/Ubuntu-based systems
    sudo apt install lm-sensors radeontop
  
    # For Red Hat/CentOS-based systems
    sudo yum install lm_sensors radeontop
  
    # For Arch Linux
    sudo pacman -S lm_sensors radeontop
    ```
- ### Pypi

  ```bash
  pip install RadeonMaster
  ```

## Usage

- #### Initialize logging in RadeonMaster
   The radeon top first need to start the logging then only it can provide the fetch the data .
   ```python
   import RadeonMaster
   gpu = RadeonMaster.GPU()
   ```
   It will start the threading of shell exicution to log the data.

> [!IMPORTANT]
> Don't again and again call the class ```GPU()``` , bcoz it again exicute the script leads to get unstable

- #### get_available_gpus()
  ```python
  import RadeonMaster
  gpus = RadeonMaster.get_available_gpus()
  print(gpus)
  ```
  **Output**
  ```bash
  [
    {
      "Bus address": "00:02.0",
      "Name": "Intel Corporation HD Graphics 530 (rev 06)",
      "Type": "Intergrated gpu"
    },
    {
      "Bus address": "01:00.0",
      "Name": "Advanced Micro Devices, Inc. [AMD/ATI] Oland [Radeon HD 8570 / R5 430 OEM / R7 240/340 / Radeon 520 OEM] (rev 87)",
      "Type": "Dedicated gpu"
    }
  ]
  ```
- #### get_temp()

  This function return the temparature by the bus address

  ```python
  import RadeonMaster
  print(RadeonMaster.get_temp('0100')) # replace the '0100` with actual bus address.
  ```
  
- #### get_output()
  It will return a list that contains all the iformation about radeon GPU .
  
  - parameter: 
    This function have ```bus_address``` as parameter.
    
  - Examples:
    #### 1.Using without bus address:
    
     - **code**:
       
      ```python
      import RadeonMaster
      gpu = RadeonMaster.GPU()
      info = gpu.get_output()
      print(info)
      gpu.stop_logging()
      
      #It will give the list with all GPU with all informations
      ```
    - **Output**:
      
     ```bash
    [{'bus address': '01:00.0', 'GPU type': 'Dedicated gpu', 'GPU name': 'Advanced Micro Devices, Inc. [AMD/ATI] Oland [Radeon HD 8570 / R5 430 OEM / R7 240/340 / Radeon 520 OEM] (rev 87)', 'GPU temp': 43.0, 'bus': '01,', 'GPU usage': '26.67%,', 'Event Engine': '0.00%,', 'Vertex Grouper + Tesselator': '0.00%,', 'Texture Addresser': '25.00%,', 'Sequencer Instruction Cache': '0.00%,', 'Shader Interpolator': '25.00%,', 'scan converter': '25.83%,', 'Primitive Assembly': '5.83%,', 'depth block': '25.83%,', 'color block': '25.83%,', 'VRAM PERCENTAGE': '13.87%', 'VRAM Used': '284.11mb,', 'VRAM Total': '2048.38mb', 'VRAM': '284.11mb, / 2048.38mb percentage : 13.87%', 'GTT PERCENTAGE': '1.21%', 'GTT Used': '24.63mb,', 'GTT Total': '2035.54mb', 'GTT': '24.63mb, / 2035.54mb percentage : 1.21%', 'Memory Clock PERCENTAGE': 'inf%', 'Memory Clock Used': 'Not found', 'Memory Clock PERCENT': 'Not found', 'Memory Clock Total': 'Not found', 'Memory Clock': 'Not found', 'Shader Clock PERCENTAGE': '46.90%', 'Shader Clock Used': '0.366ghz', 'Shader Clock Total': '0.78ghz', 'Shader Clock': '0.366ghz / 0.78ghz percentage : 46.90%'}]
     ```
    #### 2.Using with bus address:
      - **code**:  
      ```python
      import RadeonMaster
      gpu = RadeonMaster.GPU()
      info = gpu.get_output('01001')
      print(info)
      gpu.stop_logging()
      
      #It will give the information for gpu in '0100' bus address
      ```
      - **Output**:
      
     ```bash
    {'bus address': '01:00.0', 'GPU type': 'Dedicated gpu', 'GPU name': 'Advanced Micro Devices, Inc. [AMD/ATI] Oland [Radeon HD 8570 / R5 430 OEM / R7 240/340 / Radeon 520 OEM] (rev 87)', 'GPU temp': 44.0, 'bus': '01,', 'GPU usage': '22.50%,', 'Event Engine': '0.00%,', 'Vertex Grouper + Tesselator': '0.00%,', 'Texture Addresser': '20.00%,', 'Sequencer Instruction Cache': '0.00%,', 'Shader Interpolator': '20.00%,', 'scan converter': '21.67%,', 'Primitive Assembly': '3.33%,', 'depth block': '21.67%,', 'color block': '21.67%,', 'VRAM PERCENTAGE': '13.60%', 'VRAM Used': '278.63mb,', 'VRAM Total': '2048.75mb', 'VRAM': '278.63mb, / 2048.75mb percentage : 13.60%', 'GTT PERCENTAGE': '1.21%', 'GTT Used': '24.70mb,', 'GTT Total': '2041.32mb', 'GTT': '24.70mb, / 2041.32mb percentage : 1.21%', 'Memory Clock PERCENTAGE': 'inf%', 'Memory Clock Used': 'Not found', 'Memory Clock PERCENT': 'Not found', 'Memory Clock Total': 'Not found', 'Memory Clock': 'Not found', 'Shader Clock PERCENTAGE': '44.76%', 'Shader Clock Used': '0.349ghz', 'Shader Clock Total': '0.78ghz', 'Shader Clock': '0.349ghz / 0.78ghz percentage : 44.76%'}
     ```
    #### 3.Using index:
    
    - **code**:  
    ```python
    import RadeonMaster
    gpu = RadeonMaster.GPU()
    info = gpu.get_output(0)
    print(info)
    gpu.stop_logging()
    
    #It will give the information for index 0 gpu
    ```
    - **Output**:
    
     ```bash
    {'bus address': '01:00.0', 'GPU type': 'Dedicated gpu', 'GPU name': 'Advanced Micro Devices, Inc. [AMD/ATI] Oland [Radeon HD 8570 / R5 430 OEM / R7 240/340 / Radeon 520 OEM] (rev 87)', 'GPU temp': 44.0, 'bus': '01,', 'GPU usage': '22.50%,', 'Event Engine': '0.00%,', 'Vertex Grouper + Tesselator': '0.00%,', 'Texture Addresser': '20.00%,', 'Sequencer Instruction Cache': '0.00%,', 'Shader Interpolator': '20.00%,', 'scan converter': '21.67%,', 'Primitive Assembly': '3.33%,', 'depth block': '21.67%,', 'color block': '21.67%,', 'VRAM PERCENTAGE': '13.60%', 'VRAM Used': '278.63mb,', 'VRAM Total': '2048.75mb', 'VRAM': '278.63mb, / 2048.75mb percentage : 13.60%', 'GTT PERCENTAGE': '1.21%', 'GTT Used': '24.70mb,', 'GTT Total': '2041.32mb', 'GTT': '24.70mb, / 2041.32mb percentage : 1.21%', 'Memory Clock PERCENTAGE': 'inf%', 'Memory Clock Used': 'Not found', 'Memory Clock PERCENT': 'Not found', 'Memory Clock Total': 'Not found', 'Memory Clock': 'Not found', 'Shader Clock PERCENTAGE': '44.76%', 'Shader Clock Used': '0.349ghz', 'Shader Clock Total': '0.78ghz', 'Shader Clock': '0.349ghz / 0.78ghz percentage : 44.76%'}
     ```
    #### 4.get particular info:
      In this example only provided the 'VRAM Used' . check [Data provided by RadeonMaster](#data-provided-by-radeonmaster) or use ```print(RadeonMaster.keywords)``` to get all keywords 
      - **code**:  
      ```python
      import RadeonMaster
      gpu = RadeonMaster.GPU()
      info = gpu.get_output('0100')
      info = info['VRAM Used']
      print(info)
      gpu.stop_logging()
      
      ```
      - **Output**:
      
     ```bash
      200.04mb
     ```

 - #### continuos_output()

   continuos_output used to get iterating realtime output
   parameters: ```bus_address``` , ```interval``` , ```out_range```
   
   - ##### bus_address()
     only using bus address give output until the program stop or use the ```stop_logging()```
     
     ```python
     import RadeonMaster
     gpu = RadeonMaster.GPU()
     for data in gpu.continuos_output('0100'):
       print(data)
     ```
     **output**:
     ```bash
      {'bus address': '01:00.0', 'GPU type': 'Dedicated gpu', 'GPU name': 'Advanced Micro Devices, Inc. [AMD/ATI] Oland [Radeon HD 8570 / R5 430 OEM / R7 240/340 / Radeon 520 OEM] (rev 87)', 'GPU temp': 43.0, 'bus': '01,', 'GPU usage': '24.17%,', 'Event Engine': '0.00%,', 'Vertex Grouper + Tesselator': '0.00%,', 'Texture Addresser': '22.50%,', 'Sequencer Instruction Cache': '0.00%,', 'Shader Interpolator': '23.33%,', 'scan converter': '23.33%,', 'Primitive Assembly': '5.83%,', 'depth block': '24.17%,', 'color block': '24.17%,', 'VRAM PERCENTAGE': '13.48%', 'VRAM Used': '276.06mb,', 'VRAM Total': '2047.92mb', 'VRAM': '276.06mb, / 2047.92mb percentage : 13.48%', 'GTT PERCENTAGE': '1.21%', 'GTT Used': '24.79mb,', 'GTT Total': '2048.76mb', 'GTT': '24.79mb, / 2048.76mb percentage : 1.21%', 'Memory Clock PERCENTAGE': 'inf%', 'Memory Clock Used': 'Not found', 'Memory Clock PERCENT': 'Not found', 'Memory Clock Total': 'Not found', 'Memory Clock': 'Not found', 'Shader Clock PERCENTAGE': '44.66%', 'Shader Clock Used': '0.348ghz', 'Shader Clock Total': '0.78ghz', 'Shader Clock': '0.348ghz / 0.78ghz percentage : 44.66%'}
      {'bus address': '01:00.0', 'GPU type': 'Dedicated gpu', 'GPU name': 'Advanced Micro Devices, Inc. [AMD/ATI] Oland [Radeon HD 8570 / R5 430 OEM / R7 240/340 / Radeon 520 OEM] (rev 87)', 'GPU temp': 43.0, 'bus': '01,', 'GPU usage': '24.17%,', 'Event Engine': '0.00%,', 'Vertex Grouper + Tesselator': '0.00%,', 'Texture Addresser': '22.50%,', 'Sequencer Instruction Cache': '0.00%,', 'Shader Interpolator': '23.33%,', 'scan converter': '23.33%,', 'Primitive Assembly': '5.83%,', 'depth block': '24.17%,', 'color block': '24.17%,', 'VRAM PERCENTAGE': '13.48%', 'VRAM Used': '276.06mb,', 'VRAM Total': '2047.92mb', 'VRAM': '276.06mb, / 2047.92mb percentage : 13.48%', 'GTT PERCENTAGE': '1.21%', 'GTT Used': '24.79mb,', 'GTT Total': '2048.76mb', 'GTT': '24.79mb, / 2048.76mb percentage : 1.21%', 'Memory Clock PERCENTAGE': 'inf%', 'Memory Clock Used': 'Not found', 'Memory Clock PERCENT': 'Not found', 'Memory Clock Total': 'Not found', 'Memory Clock': 'Not found', 'Shader Clock PERCENTAGE': '44.66%', 'Shader Clock Used': '0.348ghz', 'Shader Clock Total': '0.78ghz', 'Shader Clock': '0.348ghz / 0.78ghz percentage : 44.66%'}
      {'bus address': '01:00.0', 'GPU type': 'Dedicated gpu', 'GPU name': 'Advanced Micro Devices, Inc. [AMD/ATI] Oland [Radeon HD 8570 / R5 430 OEM / R7 240/340 / Radeon 520 OEM] (rev 87)', 'GPU temp': 44.0, 'bus': '01,', 'GPU usage': '0.83%,', 'Event Engine': '0.00%,', 'Vertex Grouper + Tesselator': '0.00%,', 'Texture Addresser': '0.83%,', 'Sequencer Instruction Cache': '0.00%,', 'Shader Interpolator': '0.83%,', 'scan converter': '0.83%,', 'Primitive Assembly': '0.00%,', 'depth block': '0.83%,', 'color block': '0.83%,', 'VRAM PERCENTAGE': '13.48%', 'VRAM Used': '276.06mb,', 'VRAM Total': '2047.92mb', 'VRAM': '276.06mb, / 2047.92mb percentage : 13.48%', 'GTT PERCENTAGE': '1.22%', 'GTT Used': '24.91mb,', 'GTT Total': '2041.8mb', 'GTT': '24.91mb, / 2041.8mb percentage : 1.22%', 'Memory Clock PERCENTAGE': 'inf%', 'Memory Clock Used': 'Not found', 'Memory Clock PERCENT': 'Not found', 'Memory Clock Total': 'Not found', 'Memory Clock': 'Not found', 'Shader Clock PERCENTAGE': '39.32%', 'Shader Clock Used': '0.307ghz', 'Shader Clock Total': '0.78ghz', 'Shader Clock': '0.307ghz / 0.78ghz percentage : 39.32%'}
      {'bus address': '01:00.0', 'GPU type': 'Dedicated gpu', 'GPU name': 'Advanced Micro Devices, Inc. [AMD/ATI] Oland [Radeon HD 8570 / R5 430 OEM / R7 240/340 / Radeon 520 OEM] (rev 87)', 'GPU temp': 43.0, 'bus': '01,', 'GPU usage': '2.50%,', 'Event Engine': '0.00%,', 'Vertex Grouper + Tesselator': '0.00%,', 'Texture Addresser': '2.50%,', 'Sequencer Instruction Cache': '0.00%,', 'Shader Interpolator': '2.50%,', 'scan converter': '2.50%,', 'Primitive Assembly': '0.83%,', 'depth block': '2.50%,', 'color block': '2.50%,', 'VRAM PERCENTAGE': '13.55%', 'VRAM Used': '277.43mb,', 'VRAM Total': '2047.45mb', 'VRAM': '277.43mb, / 2047.45mb percentage : 13.55%', 'GTT PERCENTAGE': '1.22%', 'GTT Used': '24.93mb,', 'GTT Total': '2043.44mb', 'GTT': '24.93mb, / 2043.44mb percentage : 1.22%', 'Memory Clock PERCENTAGE': 'inf%', 'Memory Clock Used': 'Not found', 'Memory Clock PERCENT': 'Not found', 'Memory Clock Total': 'Not found', 'Memory Clock': 'Not found', 'Shader Clock PERCENTAGE': '40.38%', 'Shader Clock Used': '0.315ghz', 'Shader Clock Total': '0.78ghz', 'Shader Clock': '0.315ghz / 0.78ghz percentage : 40.38%'}
      {'bus address': '01:00.0', 'GPU type': 'Dedicated gpu', 'GPU name': 'Advanced Micro Devices, Inc. [AMD/ATI] Oland [Radeon HD 8570 / R5 430 OEM / R7 240/340 / Radeon 520 OEM] (rev 87)', 'GPU temp': 43.0, 'bus': '01,', 'GPU usage': '15.83%,', 'Event Engine': '0.00%,', 'Vertex Grouper + Tesselator': '0.83%,', 'Texture Addresser': '13.33%,', 'Sequencer Instruction Cache': '0.00%,', 'Shader Interpolator': '14.17%,', 'scan converter': '15.00%,', 'Primitive Assembly': '5.83%,', 'depth block': '15.00%,', 'color block': '15.00%,', 'VRAM PERCENTAGE': '13.46%', 'VRAM Used': '275.73mb,', 'VRAM Total': '2048.51mb', 'VRAM': '275.73mb, / 2048.51mb percentage : 13.46%', 'GTT PERCENTAGE': '1.23%', 'GTT Used': '25.17mb,', 'GTT Total': '2046.34mb', 'GTT': '25.17mb, / 2046.34mb percentage : 1.23%', 'Memory Clock PERCENTAGE': 'inf%', 'Memory Clock Used': 'Not found', 'Memory Clock PERCENT': 'Not found', 'Memory Clock Total': 'Not found', 'Memory Clock': 'Not found', 'Shader Clock PERCENTAGE': '45.83%', 'Shader Clock Used': '0.358ghz', 'Shader Clock Total': '0.78ghz', 'Shader Clock': '0.358ghz / 0.78ghz percentage : 45.83%'}
      {'bus address': '01:00.0', 'GPU type': 'Dedicated gpu', 'GPU name': 'Advanced Micro Devices, Inc. [AMD/ATI] Oland [Radeon HD 8570 / R5 430 OEM / R7 240/340 / Radeon 520 OEM] (rev 87)', 'GPU temp': 42.0, 'bus': '01,', 'GPU usage': '0.00%,', 'Event Engine': '0.00%,', 'Vertex Grouper + Tesselator': '0.00%,', 'Texture Addresser': '0.00%,', 'Sequencer Instruction Cache': '0.00%,', 'Shader Interpolator': '0.00%,', 'scan converter': '0.00%,', 'Primitive Assembly': '0.00%,', 'depth block': '0.00%,', 'color block': '0.00%,', 'VRAM PERCENTAGE': '13.35%', 'VRAM Used': '273.49mb,', 'VRAM Total': '2048.61mb', 'VRAM': '273.49mb, / 2048.61mb percentage : 13.35%', 'GTT PERCENTAGE': '1.24%', 'GTT Used': '25.27mb,', 'GTT Total': '2037.9mb', 'GTT': '25.27mb, / 2037.9mb percentage : 1.24%', 'Memory Clock PERCENTAGE': 'inf%', 'Memory Clock Used': 'Not found', 'Memory Clock PERCENT': 'Not found', 'Memory Clock Total': 'Not found', 'Memory Clock': 'Not found', 'Shader Clock PERCENTAGE': '38.89%', 'Shader Clock Used': '0.303ghz', 'Shader Clock Total': '0.78ghz', 'Shader Clock': '0.303ghz / 0.78ghz percentage : 38.89%'}
      {'bus address': '01:00.0', 'GPU type': 'Dedicated gpu', 'GPU name': 'Advanced Micro Devices, Inc. [AMD/ATI] Oland [Radeon HD 8570 / R5 430 OEM / R7 240/340 / Radeon 520 OEM] (rev 87)', 'GPU temp': 42.0, 'bus': '01,', 'GPU usage': '0.83%,', 'Event Engine': '0.00%,', 'Vertex Grouper + Tesselator': '0.00%,', 'Texture Addresser': '0.83%,', 'Sequencer Instruction Cache': '0.00%,', 'Shader Interpolator': '0.83%,', 'scan converter': '0.83%,', 'Primitive Assembly': '0.83%,', 'depth block': '0.83%,', 'color block': '0.83%,', 'VRAM PERCENTAGE': '13.35%', 'VRAM Used': '273.49mb,', 'VRAM Total': '2048.61mb', 'VRAM': '273.49mb, / 2048.61mb percentage : 13.35%', 'GTT PERCENTAGE': '1.24%', 'GTT Used': '25.37mb,', 'GTT Total': '2045.97mb', 'GTT': '25.37mb, / 2045.97mb percentage : 1.24%', 'Memory Clock PERCENTAGE': 'inf%', 'Memory Clock Used': 'Not found', 'Memory Clock PERCENT': 'Not found', 'Memory Clock Total': 'Not found', 'Memory Clock': 'Not found', 'Shader Clock PERCENTAGE': '38.89%', 'Shader Clock Used': '0.303ghz', 'Shader Clock Total': '0.78ghz', 'Shader Clock': '0.303ghz / 0.78ghz percentage : 38.89%'}
      {'bus address': '01:00.0', 'GPU type': 'Dedicated gpu', 'GPU name': 'Advanced Micro Devices, Inc. [AMD/ATI] Oland [Radeon HD 8570 / R5 430 OEM / R7 240/340 / Radeon 520 OEM] (rev 87)', 'GPU temp': 43.0, 'bus': '01,', 'GPU usage': '0.83%,', 'Event Engine': '0.00%,', 'Vertex Grouper + Tesselator': '0.00%,', 'Texture Addresser': '0.83%,', 'Sequencer Instruction Cache': '0.00%,', 'Shader Interpolator': '0.83%,', 'scan converter': '0.83%,', 'Primitive Assembly': '0.00%,', 'depth block': '0.83%,', 'color block': '0.83%,', 'VRAM PERCENTAGE': '13.42%', 'VRAM Used': '274.86mb,', 'VRAM Total': '2048.14mb', 'VRAM': '274.86mb, / 2048.14mb percentage : 13.42%', 'GTT PERCENTAGE': '1.24%', 'GTT Used': '25.38mb,', 'GTT Total': '2046.77mb', 'GTT': '25.38mb, / 2046.77mb percentage : 1.24%', 'Memory Clock PERCENTAGE': 'inf%', 'Memory Clock Used': 'Not found', 'Memory Clock PERCENT': 'Not found', 'Memory Clock Total': 'Not found', 'Memory Clock': 'Not found', 'Shader Clock PERCENTAGE': '40.06%', 'Shader Clock Used': '0.313ghz', 'Shader Clock Total': '0.78ghz', 'Shader Clock': '0.313ghz / 0.78ghz percentage : 40.06%'}
     .....
     ```
   - ##### out_range()
     Using the ```out_range``` it only give for that range
     
     ```python
     import RadeonMaster
     gpu = RadeonMaster.GPU()
     for data in gpu.continuos_output('0100',out_range=2):
       print(data)
     ```
     **output**:
     ```bash
     {'bus address': '01:00.0', 'GPU type': 'Dedicated gpu', 'GPU name': 'Advanced Micro Devices, Inc. [AMD/ATI] Oland [Radeon HD 8570 / R5 430 OEM / R7 240/340 / Radeon 520 OEM] (rev 87)', 'GPU temp': 43.0, 'bus': '01,', 'GPU usage': '20.83%,', 'Event Engine': '0.00%,', 'Vertex Grouper + Tesselator': '0.83%,', 'Texture Addresser': '15.83%,', 'Sequencer Instruction Cache': '0.00%,', 'Shader Interpolator': '17.50%,', 'scan converter': '18.33%,', 'Primitive Assembly': '6.67%,', 'depth block': '19.17%,', 'color block': '19.17%,', 'VRAM PERCENTAGE': '13.84%', 'VRAM Used': '283.51mb,', 'VRAM Total': '2048.48mb', 'VRAM': '283.51mb, / 2048.48mb percentage : 13.84%', 'GTT PERCENTAGE': '1.21%', 'GTT Used': '24.66mb,', 'GTT Total': '2038.02mb', 'GTT': '24.66mb, / 2038.02mb percentage : 1.21%', 'Memory Clock PERCENTAGE': 'inf%', 'Memory Clock Used': 'Not found', 'Memory Clock PERCENT': 'Not found', 'Memory Clock Total': 'Not found', 'Memory Clock': 'Not found', 'Shader Clock PERCENTAGE': '44.34%', 'Shader Clock Used': '0.346ghz', 'Shader Clock Total': '0.78ghz', 'Shader Clock': '0.346ghz / 0.78ghz percentage : 44.34%'}
     {'bus address': '01:00.0', 'GPU type': 'Dedicated gpu', 'GPU name': 'Advanced Micro Devices, Inc. [AMD/ATI] Oland [Radeon HD 8570 / R5 430 OEM / R7 240/340 / Radeon 520 OEM] (rev 87)', 'GPU temp': 44.0, 'bus': '01,', 'GPU usage': '20.83%,', 'Event Engine': '0.00%,', 'Vertex Grouper + Tesselator': '0.83%,', 'Texture Addresser': '15.83%,', 'Sequencer Instruction Cache': '0.00%,', 'Shader Interpolator': '17.50%,', 'scan converter': '18.33%,', 'Primitive Assembly': '6.67%,', 'depth block': '19.17%,', 'color block': '19.17%,', 'VRAM PERCENTAGE': '13.84%', 'VRAM Used': '283.51mb,', 'VRAM Total': '2048.48mb', 'VRAM': '283.51mb, / 2048.48mb percentage : 13.84%', 'GTT PERCENTAGE': '1.21%', 'GTT Used': '24.66mb,', 'GTT Total': '2038.02mb', 'GTT': '24.66mb, / 2038.02mb percentage : 1.21%', 'Memory Clock PERCENTAGE': 'inf%', 'Memory Clock Used': 'Not found', 'Memory Clock PERCENT': 'Not found', 'Memory Clock Total': 'Not found', 'Memory Clock': 'Not found', 'Shader Clock PERCENTAGE': '44.34%', 'Shader Clock Used': '0.346ghz', 'Shader Clock Total': '0.78ghz', 'Shader Clock': '0.346ghz / 0.78ghz percentage : 44.34%'}
     ```
