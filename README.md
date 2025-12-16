This repository contains the artifacts for the paper **Pitfalls for Security Isolation in Multi-CPU Systems**, published at NDSS 2026.
All experiments have been performed on Ubuntu 24.04.

## Directory layout and files
The experiments-st-final.zip contains all ST experiments. 
Do not unpack it manually, the STM32CubeIDE can do that for you. See **Setting up the ST workspace**.
In the `experiments-nrf5340` folder, you will find two subfolders, `peripheral` and `hci_ipc`.
These are the names of the zephyr samples that the experiments are based on. 
They contain the modified files over the samples provided by zephyr.

## Environment setup
You will need a STM32H755-Nucleo development board for the ST experiments, and a nRF5340 development board for the real-world experiment.

### Setting up the ST workspace
Install the STM32CubeIDE.
Import the experiments-st-final.zip file: **File** -> **Import**. 
Select **Projects from Folder or Archive** under **General**, then press **Next**.
Click on **Archive...** and select the provided \verb|experiments-st.zip|.
Make sure **Search for nested projects** and **Detect and configure project natures** are ticked.
In the import selection window, make sure that **only the Eclipse Projects are selected for import, and nothing else**.
Then press **Finish**.
If everything worked correctly, you should see five projects on the left in the project view. 
Now for each project, you need to setup the M4 and the M7 project. 
To do that, click on the arrow to expand the folder structure, then **right click on CM4 and CM7 respectively** in each folder structure and select **Import as Project**.
This will transform the respective folder in a project (it now has an \verb|IDE| icon), which you can build. 
Confirm that you can build it by right-clicking on the project and pressing **Clean Project**, then **Build Project**.
The ST setup is complete once you built all the projects.

### Setting up zephyr
Follow the [zephyr getting started guide](https://docs.zephyrproject.org/latest/develop/getting_started/index.html).
Then, download `nrfutil` from [here](https://www.nordicsemi.com/Products/Development-tools/nRF-Util/Download).
Make sure it is in your path.
Install the `device` command: `nrfutil install device`.
Install the nrf command line tools from [here](https://www.nordicsemi.com/Products/Development-tools/nRF-Command-Line-Tools/Download).

### Running experiment E1 + E2
1. Click on the arrow of the **empty-h755-mpu** project. This
opens the folder structure.
2. Right click on the **empty-h755-mpu CM7** project, then
run **Clean Project**. Afterwards, run **Build Project**.
3. Repeat 2. for the **empty-h755-mpu CM4** project.
4. Right click on the **empty-h755-mpu CM7** project, se-
lect **Debug As** → **Debug Configurations...**.
5. On the left hand side, you see numerous debug configura-
tions. Select **empty-h755-mpu CM7**, then press **Debug**.
This downloads both the M7 and the M4 firmware to
their respective CPU and starts a debugging session for
the M7. It breaks on the first line in the M7 main function,
where the M4 has not started yet.
6. Press **Resume** in the toolbar at the top of the window.

Expected results: For successful E1 reproduction, **Direct Access Worked** must not be in the UART output.
For successful E2 reproduction, **E2 worked** must bi in the UART output.

### Running experiment E3
1. Click on the arrow of the **Communication-DataLeak** project. This
opens the folder structure.
2. Right click on the **Communication-DataLeak CM7** project, then
run **Clean Project**. Afterwards, run **Build Project**.
3. Repeat 2. for the **Communication-DataLeak CM4** project.
4. Right click on the **Communication-DataLeak CM7** project, se-
lect **Debug As** → **Debug Configurations...**.
5. On the left hand side, you see numerous debug configura-
tions. Select **Communication-DataLeak CM7**, then press **Debug**.
This downloads both the M7 and the M4 firmware to
their respective CPU and starts a debugging session for
the M7. It breaks on the first line in the M7 main function,
where the M4 has not started yet.
6. Press **Resume** in the toolbar at the top of the window.

Expected results: For successful reproduction, **E3 worked** must be in the UART output.

### Running experiment E4+E5
Make sure that line 35 in main.c in the M4 source tree (under `Comm...-CodeExec_CM4/Core/Src/main.c`) is not commented.

1. Click on the arrow of the **Communication-CodeExec** project. This
opens the folder structure.
2. Right click on the **Communication-CodeExec CM7** project, then
run **Clean Project**. Afterwards, run **Build Project**.
3. Repeat 2. for the **Communication-CodeExec CM4** project.
4. Right click on the **Communication-CodeExec CM7** project, se-
lect **Debug As** → **Debug Configurations...**.
5. On the left hand side, you see numerous debug configura-
tions. Select **Communication-CodeExec CM7**, then press **Debug**.
This downloads both the M7 and the M4 firmware to
their respective CPU and starts a debugging session for
the M7. It breaks on the first line in the M7 main function,
where the M4 has not started yet.
6. Press **Resume** in the toolbar at the top of the window.
7. To execute E5, comment line 35 in **main.c** in the M4 source tree (under **Comm...-CodeExec_CM4/Core/Src/main.c**) and rerun steps 1-6. Check Results E5 at this point.

Expected results: For successful E4 reproduction, **E5 worked** must **not** be present in the output. 
For successful E5 reproduction, **E5 worked** must be present in the output. 

### Running experiment E6
1. Click on the arrow of the **empty-h755-peripherals** project. This
opens the folder structure.
2. Right click on the **empty-h755-peripherals CM7** project, then
run **Clean Project**. Afterwards, run **Build Project**.
3. Repeat 2. for the **empty-h755-peripherals CM4** project.
4. Right click on the **empty-h755-peripherals CM7** project, se-
lect **Debug As** → **Debug Configurations...**.
5. On the left hand side, you see numerous debug configura-
tions. Select **empty-h755-peripherals CM7**, then press **Debug**.
This downloads both the M7 and the M4 firmware to
their respective CPU and starts a debugging session for
the M7. It breaks on the first line in the M7 main function,
where the M4 has not started yet.
6. Press **Resume** in the toolbar at the top of the window.

Expected results:**E6 worked** must be present in the output. 

### Running experiment E7+E8
Make sure that line 30 in main.c in the M4 source tree (under `Comm...-CodeExec_CM4/Core/Src/main.c`) is not commented.

1. Click on the arrow of the **Communication-CodeExec** project. This
opens the folder structure.
2. Right click on the **Communication-CodeExec CM7** project, then
run **Clean Project**. Afterwards, run **Build Project**.
3. Repeat 2. for the **Communication-CodeExec CM4** project.
4. Right click on the **Communication-CodeExec CM7** project, se-
lect **Debug As** → **Debug Configurations...**.
5. On the left hand side, you see numerous debug configura-
tions. Select **Communication-CodeExec CM7**, then press **Debug**.
This downloads both the M7 and the M4 firmware to
their respective CPU and starts a debugging session for
the M7. It breaks on the first line in the M7 main function,
where the M4 has not started yet.
6. Press **Resume** in the toolbar at the top of the window.
7. To execute E5, comment line 35 in **main.c** in the M4 source tree (under **Comm...-CodeExec_CM4/Core/Src/main.c**) and rerun steps 1-6. Check Results E5 at this point.

Expected results: For successful E7 reproduction, **E8 worked** must **not** be present in the output. 
For successful E8 reproduction, **E8 worked** must be present in the output. 

### Running experiment E9+E10
To build the app core target, navigate to `zephyr/samples/bluetooth/peripheral`.
Replace the `prj.conf` with the one provided from us, and replace the `src/main.c` as well with our provided file.
To build the net core target, navigate to `zephyr/samples/bluetooth/hci_ipc` and replace `src/main.c` with the provided main file.
Build the app core target with the following command (while still in the `peripheral` folder): `west build -p -b nrf5340dk/nrf5340/cpuapp .`
Similarly, build the net core target with the following command (while in the `hci_ipc` folder): `west build -p -b nrf5340dk/nrf5340/cpunet .` in `samples/bluetooth/hci_ipc`.
You can flash the firmwares to the board with `west flash`.
Experiment 9 is successful if, in the left terminal, you see the string: `secret data: secret`.
If there is any other value, the attack failed.
Experiment 10 is successful if, in the right terminal, you can see the string `The attack worked!`.
