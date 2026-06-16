# stm32-quectel-eg915-driver

This firmware enables an STM32G0B0RE microcontroller to manage a Quectel EG915U-LA modem. The primary function is to establish a connection to an MQTT broker for bidirectional communication, facilitating several key tasks for a connected Control Board.

### Project Description

**Firmware Version:** 1.0.0

The module is designed to perform three core functions:
1.  **Data Reporting:** Transmit operational statistics to a Firebase server.
2.  **Content Management:** Download barcode (EAN) data from a server and transfer it to the Control Board.
3.  **Remote Updates (FOTA):** Perform Firmware-Over-The-Air (FOTA) updates on the connected Control Board.

### Hardware Configuration
*   **Microcontroller:** STM32G0B0RET6
*   **Cellular Modem:** QUECTEL EG915U-LA
*   **SIM:** 1nce SIM card with a static IP address

### Development Environment
*   **IDE:** STM32CubeIDE (v1.18.0)
*   **Framework:** STM32CubeG0 Firmware Package (v1.6.2)
*   **Compiler:** arm-none-eabi-gcc
*   **Target MCU:** STM32G0B0RETx

## How to Build the Project

Follow these steps to set up the development environment and open the project in STM32CubeIDE.

### Prerequisites
1.  **Install STM32CubeIDE:** Download and install the latest version of [STM32CubeIDE](https://www.st.com/en/development-tools/stm32cubeide.html) for your operating system.
2.  **Install the STM32G0 HAL:** The project requires the STM32CubeG0 firmware package. It should be installed automatically through the IDE's package manager. If not, you can download it manually from the [STM32CubeG0 page](https://www.st.com/en/embedded-software/stm32cubeg0.html) and install it via `Help > Embedded Software Packages` in the IDE.

![Imagen de package_1](imgs/package_1.png "package_1")

![Imagen de package_2](imgs/package_2.png "package_2")

3.  **Clone the Repository:** Get the source code by cloning the repository to your local machine using Git:
    ```bash
    git clone https://github.com/ChillitJSMR/CHILLIT_SIM.git
    ```
    *Alternatively, you can use a GUI client like [Sourcetree](https://www.sourcetreeapp.com).*

### Importing the Project
1.  **Launch STM32CubeIDE** and select the workspace located at `.../CHILLIT_SIM/_STM32G0B0RE/_workspaceSTM32` within the cloned repository.

![Imagen de workspace](imgs/workspace.png "workspace")    

2.  Go to `File > Import...`.

![Imagen de import](imgs/import.png "import")

3.  In the import dialog, expand `General`, select `Existing Projects into Workspace`, and click `Next`.

![Imagen de projects_into_workspace](imgs/projects_into_workspace.png "projects_into_workspace")

4.  Configure the import:
    *   **Select root directory:** Browse to the root directory (_workspaceSTM32) of the cloned repository (the folder containing the `Core/`, `Drivers/`, etc. folders).
    *   **Projects:** Select `commQuectelv00`.
    *   Click **Finish**.

![Imagen de root_directory](imgs/root_directory.png "root_directory")

5.  The project will now be imported and appear in the Project Explorer. You can build it (`Debug Mode default`) by right-clicking on the project and selecting `Build Project`.

![Imagen de build_project](imgs/build_project.png "build_project")

### Compiling and Flashing the Project (Release Mode)

This section describes how to build the project for Release and flash it to the target microcontroller.

#### 1. Set the Build Configuration
*   Go to `Project > Build Configurations > Set Active > Release`.
*   This tells the IDE to build with optimizations and without debug symbols.

![Imagen de release_mode](imgs/release_mode.png "release_mode")

#### 2. Build the Project
*   Right-click on the `commQuectelv00` project in the Project Explorer.
*   Select `Build Project`. The IDE will compile the code and generate the binary files.

#### 3. Locate the Binary File
*   After a successful build, the generated `.elf` file can be found in the `Release/` folder within your project directory.

![Imagen de elf_file](imgs/elf_file.png "elf_file")

#### 4. Flash the Firmware to the MCU
*   Ensure the **ST-LINK programmer is connected** to the SIM Module board and your computer.
*   Go to `Run > Run As > 1 STM32 C/C++ Application`.

![Imagen de run_1](imgs/run_1.png "run_1")

*   A configuration dialog will appear. Verify the following settings:
    *   **C/C++ Application:** Browse and select the `commQuectelv00.elf` file from the `Release/` folder.
    *   **Build Configuration:** `Release`
*   Click `OK` to begin the flashing process.

![Imagen de run_2](imgs/run_2.png "run_2")

*   The console will output the flashing progress. A successful flash will be confirmed by a message in the console.

![Imagen de flash_ok](imgs/flash_ok.png "flash_ok")

### Flashing the Firmware using STM32CubeProgrammer

This section explains how to flash the compiled firmware (ELF file) to the target microcontroller using the standalone STM32CubeProgrammer tool.

#### 1. Download and Install the Tool
*   Download **STM32CubeProgrammer** for your operating system from the official STMicroelectronics website:
    *   [STM32CubeProgrammer Download Page](https://www.st.com/en/development-tools/stm32cubeprog.html)
*   Install the application and launch it.

![Imagen de stm32programmer](imgs/stm32programmer.png "stm32programmer")

#### 2. Connect and Program the MCU
1.  **Select the ELF File:**
    *   In the main interface, navigate to the **Erasing and Programming** section.
    *   Click the `Browse` button next to "File path" and select the `.elf` file from the `Release_Firmware_1_7_1` folder in the project repository.

![Imagen de erasing_programming_1](imgs/erasing_programming_1.png "erasing_programming_1")

2.  **Establish Connection:**
    *   Ensure the **ST-LINK debugger is properly connected** to both the SIM Module board and your computer.
    *   Click the `Connect` button. The tool should establish a connection with the microcontroller.

3.  **Erase the Memory:**
    *   Click `Full chip erase` to clear the microcontroller's flash memory. Wait for the operation to complete.

4.  **Program the Firmware:**
    *   Click `Start Programming` to flash the new firmware.
    *   Monitor the log window for progress. A message confirming successful programming will appear upon completion.

![Imagen de erasing_programming_2](imgs/erasing_programming_2.png "erasing_programming_2")
