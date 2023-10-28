# PSoC&trade; 4: MSCLP multitouch mutual-capacitance touchpad tuning

This code example demonstrates how to use the CAPSENSE&trade; middleware to detect two finger touch positions and gesture on a mutual-capacitance-based touchpad widget in PSoC&trade; 4 devices with multi sense converter low power (MSCLP).

In addition, this code example explains how to manually tune the mutual-capacitance-based touchpad for optimum performance with respect to parameters such as reliability, power consumption, response time, and linearity using the CSX-RM sensing technique and CAPSENSE&trade; tuner GUI. Here, CAPSENSE&trade; crosspoint (CSX) represents the mutual-capacitance sensing technique and RM represents the ratiometric method.

[View this README on GitHub.](https://github.com/Infineon/mtb-example-psoc4-msclp-csx-touchpad)

[Provide feedback on this code example.](https://cypress.co1.qualtrics.com/jfe/form/SV_1NTns53sK2yiljn?Q_EED=eyJVbmlxdWUgRG9jIElkIjoiQ0UyMzUzMzkiLCJTcGVjIE51bWJlciI6IjAwMi0zNTMzOSIsIkRvYyBUaXRsZSI6IlBTb0MmdHJhZGU7IDQ6IE1TQ0xQIG11bHRpdG91Y2ggbXV0dWFsLWNhcGFjaXRhbmNlIHRvdWNocGFkIHR1bmluZyIsInJpZCI6Inlhc2h2aSIsIkRvYyB2ZXJzaW9uIjoiMi4xLjAiLCJEb2MgTGFuZ3VhZ2UiOiJFbmdsaXNoIiwiRG9jIERpdmlzaW9uIjoiTUNEIiwiRG9jIEJVIjoiSUNXIiwiRG9jIEZhbWlseSI6IlBTT0MifQ==)


## Requirements

- [ModusToolbox&trade;](https://www.infineon.com/modustoolbox) v3.1 or later

   > **Note:** This code example version requires ModusToolbox&trade; software version 3.1 or later, and is not backward compatible with v3.0 or older versions.

- Board support package (BSP) minimum required version: 3.1.0
- Programming language: C
- Associated parts: [PSoC&trade; 4000T](www.infineon.com/002-33949)

## Supported toolchains (make variable 'TOOLCHAIN')

- GNU Arm&reg; Embedded Compiler v11.3.1 (`GCC_ARM`) - Default value of `TOOLCHAIN`
- Arm&reg; Compiler v6.16 (`ARM`)
- IAR C/C++ Compiler v9.30.1 (`IAR`)

## Supported kits (make variable 'TARGET')

- [PSoC&trade; 4000T CAPSENSE&trade; Evaluation Kit](https://www.infineon.com/CY8CKIT-040T) (`CY8CKIT-040T`) - Default `TARGET`

## Hardware setup

This example uses the board's default configuration. See the kit user guide to ensure that the board is configured correctly.

> **Note:** The PSoC&trade; 4 kits (except [CY8CKIT-040T](https://www.infineon.com/CY8CKIT-040T) and [CY8CKIT-041S-MAX](https://www.infineon.com/CY8CKIT-041s-max)) ship with KitProg2 installed. ModusToolbox&trade; requires KitProg3. Before using this code example, make sure that the board is upgraded to KitProg3. The tool and instructions are available in the [Firmware Loader](https://github.com/Infineon/Firmware-loader) GitHub repository. If you do not upgrade, you will see an error like "unable to find CMSIS-DAP device" or "KitProg firmware is out of date".

## Software setup

This example requires no additional software or tools.

## Using the code example

Create the project and open it using one of the following:

<details><summary><b>In Eclipse IDE for ModusToolbox&trade;</b></summary>

1. Click the **New Application** link in the **Quick Panel** (or, use **File** > **New** > **ModusToolbox&trade; Application**). This launches the [Project Creator](https://www.infineon.com/ModusToolboxProjectCreator) tool.

2. Pick a kit supported by the code example from the list shown in the **Project Creator – Choose Board Support Package (BSP)** dialog.

   When you select a supported kit, the example is reconfigured automatically to work with the kit. To work with a different supported kit later, use the [Library Manager](https://www.infineon.com/ModusToolboxLibraryManager) to choose the BSP for the supported kit. You can use the Library Manager to select or update the BSP and firmware libraries used in this application. To access the Library Manager, click the link from the **Quick Panel**.

   You can also just start the application creation process again and select a different kit.

   If you want to use the application for a kit not listed here, you may need to update the source files. If the kit does not have the required resources, the application may not work.

3. In the **Project Creator - Select Application** dialog, choose the example by enabling the checkbox.

4. (Optional) Change the suggested **New Application Name**.

5. The **Application(s) Root Path** defaults to the Eclipse workspace, which is usually the desired location for the application. If you want to store the application in a different location, you can change the *Application(s) Root Path* value. Applications that share libraries must be in the same root path.

6. Click **Create** to complete the application creation process.

For more details, see the [Eclipse IDE for ModusToolbox&trade; user guide](https://www.infineon.com/MTBEclipseIDEUserGuide) (locally available at *{ModusToolbox&trade; install directory}/docs_{version}/mt_ide_user_guide.pdf*).

</details>

<details><summary><b>In command-line interface (CLI)</b></summary>

ModusToolbox&trade; provides the Project Creator as both a GUI tool and the command-line tool (*project-creator-cli*). The CLI tool can be used to create applications from a CLI terminal or from within batch files or shell scripts. This tool is available in the *{ModusToolbox&trade; install directory}/tools_{version}/project-creator/* directory.

Use a CLI terminal to invoke the "project-creator-cli" tool. On Windows, use the command-line "modus-shell" program provided in the ModusToolbox&trade; installation instead of a standard Windows command-line application. This shell provides access to all ModusToolbox&trade; tools. You can access it by typing `modus-shell` in the search box in the Windows menu. In Linux and macOS, you can use any terminal application.

The "project-creator-cli" tool has the following arguments:

Argument | Description | Required/optional
---------|-------------|-----------
`--board-id` | Defined in the `<id>` field of the [BSP](https://github.com/Infineon?q=bsp-manifest&type=&language=&sort=) manifest | Required
`--app-id`   | Defined in the `<id>` field of the [CE](https://github.com/Infineon?q=ce-manifest&type=&language=&sort=) manifest | Required
`--target-dir`| Specify the directory in which the application is to be created if you prefer not to use the default current working directory | Optional
`--user-app-name`| Specify the name of the application if you prefer to have a name other than the example's default name | Optional
<br>

The following example clones the "[CAPSENSE&trade; MSCLP mutual capacitance touchpad tuning](https://github.com/Infineon/mtb-example-psoc4-msclp-mutual-capacitance-touchpad)" application with the desired name "MSCLPMutualCapTouchpadTuning" configured for the *CY8CKIT-040T* BSP into the specified working directory, *C:/mtb_projects*:

   ```
   project-creator-cli --board-id CY8CKIT-040T --app-id mtb-example-psoc4-msclp-mutual-capacitance-touchpad --user-app-name MSCLPMutualCapTouchpadTuning --target-dir "C:/mtb_projects"
   ```

> **Note:** The project-creator-cli tool uses the `git clone` and `make getlibs` commands to fetch the repository and import the required libraries. For details, see the "Project creator tools" section of the [ModusToolbox&trade; user guide](https://www.infineon.com/ModusToolboxUserGuide) (locally available at *{ModusToolbox&trade; install directory}/docs_{version}/mtb_user_guide.pdf*).

To work with a different supported kit later, use the [Library Manager](https://www.infineon.com/ModusToolboxLibraryManager) to choose the BSP for the supported kit. You can invoke the Library Manager GUI tool from the terminal by using the `make library-manager` command or use the Library Manager CLI tool (library-manager-cli) to change the BSP.

The "library-manager-cli" tool has the following arguments:

Argument | Description | Required/optional
---------|-------------|-----------
`--add-bsp-name` | Name of the BSP that should be added to the application | Required
`--set-active-bsp` | Name of the BSP that should be as active BSP for the application | Required
`--add-bsp-version`| Specify the version of the BSP that should be added to the application if you do not wish to use the latest from manifest | Optional
`--add-bsp-location`| Specify the location of the BSP (local/shared) if you prefer to add the BSP in a shared path | Optional

<br />

The following example adds the CY8CKIT-040T BSP to the already created application and makes it the active BSP for the app:

   ```
   library-manager-cli --project "C:/mtb_projects/MSCLPMutualCapTouchpadTuning" --add-bsp-name CY8CKIT-040T --add-bsp-version "latest-v3.X" --add-bsp-location "local"

   library-manager-cli --project "C:/mtb_projects/MSCLPMutualCapTouchpadTuning" --set-active-bsp APP_CY8CKIT-040T
   ```

</details>

<details><summary><b>In third-party IDEs</b></summary>

Use one of the following options:

- **Use the standalone [Project Creator](https://www.infineon.com/ModusToolboxProjectCreator) tool:**

   1. Launch Project Creator from the Windows Start menu or from *{ModusToolbox&trade; install directory}/tools_{version}/project-creator/project-creator.exe*.

   2. In the initial **Choose Board Support Package** screen, select the BSP, and click **Next**.

   3. In the **Select Application** screen, select the appropriate IDE from the **Target IDE** drop-down menu.

   4. Click **Create** and follow the instructions printed in the bottom pane to import or open the exported project in the respective IDE.

<br>

- **Use command-line interface (CLI):**

   1. Follow the instructions from the **In command-line interface (CLI)** section to create the application, and then import the libraries using the `make getlibs` command.

   2. Export the application to a supported IDE using the `make <ide>` command.

   3. Follow the instructions displayed in the terminal to create or import the application as an IDE project.

For a list of supported IDEs and more details, see the "Exporting to IDEs" section of the [ModusToolbox&trade; user guide](https://www.infineon.com/ModusToolboxUserGuide) (locally available at *{ModusToolbox&trade; install directory}/docs_{version}/mtb_user_guide.pdf*).

</details>

By default, the project has the necessary settings; therefore, you can go to [Operation](#operation) to test the example. To understand the tuning process and follow the stages for this kit or your own board, go to [Tuning procedure](#tuning-procedure) and then test it using [Operation](#operation).

## Operation

1. Connect the board to your PC using the provided micro-B USB cable through the KitProg3 USB connector.

   **Figure 1. Connecting the [CY8CKIT-040T](https://www.infineon.com/CY8CKIT-040T) kit with the PC**

   <img src="images/kit_connection.png" alt="" width="400" />

2. Program the board using one of the following:

   <details><summary><b>Using Eclipse IDE for ModusToolbox&trade; software</b></summary>

      1. Select the application Project in the Project Explorer.

      2. In the **Quick Panel**, scroll down, and click **\<Application Name> Program (KitProg3_MiniProg4)**.
   </details>

   <details><summary><b>Using CLI</b></summary>

     From the terminal, execute the `make program` command to build and program the application using the default toolchain to the default target. The target and the toolchain is specified manually:
      ```
      make program TARGET=<BSP> TOOLCHAIN=<toolchain>
      ```

      Example:
      ```
      make program TARGET=CY8CKIT-040T TOOLCHAIN=GCC_ARM
      ```
   </details>

3. After programming, the application starts automatically.

4. To test the application:
   - Slide your finger over the CAPSENSE&trade; touchpad and notice that LED1 and LED3 turn ON with green color when touched and turn OFF when the finger is lifted.
      - LED1 brightness increases when finger is moved from bottom to up, with bottom row having minimum and top row having maximum brightness.
      - LED3 brightness increases when finger is moved from left to right, with left column having minimum and right column having maximum brightness.
   - Perform gestures on the Touchpad and observe LED2 colors mentioned as follows:
      - One-finger single click,  red color
      - One-finger double click, blue color
      - One-finger flick in up direction,  cyan color
      - One-finger flick in down direction,  white color
      - One-finger flick in left direction,  rose color
      - One-finger flick in right direction,  orange color
      - One-finger flick in other directions,  green color
      - Two-finger zoom in/out, violet color
      - One-finger click & drag, yellow color

      > **Note:** One-finger click and drag gesture is triggered when the finger movement follows this sequence: Touchdown → Lift Off → Touchdown → Drag .

   
5. Do the following to monitor the CAPSENSE&trade; data using the CAPSENSE&trade; tuner application:

    **Monitor data using CAPSENSE&trade; tuner**

    1. Open CAPSENSE&trade; Tuner from the tools section in the IDE **Quick Panel**.

        You can also run the CAPSENSE&trade; Tuner application in standalone mode from *{ModusToolbox&trade; install directory}/ModusToolbox/tools_{version}/capsense-configurator/capsense-tuner*. In this case, after opening the application, select **File** > **Open** and open the *design.cycapsense* file of the respective application, which is present in the *{Application root directory}/bsps/TARGET_APP_\<BSP-NAME>/config/* folder.

	     See the [ModusToolbox&trade; software user guide](https://www.infineon.com/ModusToolboxUserGuide) (locally available at *ModusToolbox&trade; install directory}/docs_{version}/mtb_user_guide.pdf*) for options to open the CAPSENSE&trade; Tuner application using the CLI.

    2. Ensure that the kit is in CMSIS-DAP bulk mode (KitProg3 status LED is ON and not blinking). To learn how to update the firmware and switch modes in KitProg3, see [Firmware-loader](https://github.com/Infineon/Firmware-loader).

    3. In the tuner application, click on the **Tuner Communication Setup** icon or select **Tools** > **Tuner Communication Setup**. In the window, select the I2C checkbox under KitProg3 and configure as follows:

       - **I2C address:** 8
       - **Sub-address:** 2 bytes
       - **Speed (kHz):** 400

        These are the same values set in the EZI2C resource.

        **Figure 2. Tuner communication setup parameters**

        <img src="images/tuner-comm-setup.png" alt="" width="600" />

    4. Click **Connect** or select **Communication** > **Connect** to establish a connection.

        **Figure 3. Establish a connection**

        <img src="images/tuner-connect.png" alt="" width="400" />

    5. Click **Start** or select **Communication** > **Start** to start data streaming from the device.

         **Figure 4. Start tuner communication**

         <img src="images/tuner-start.png" alt="" width="400" />

         The **Widget/Sensor parameters** tab gets updated with the parameters configured in the **CAPSENSE&trade; configurator** window. The tuner displays the data from the sensor in the **Widget View** and **Graph View** tabs.

6. Set the **Read Mode** to the **Synchronized** mode. Under the **Widget View** tab, you can see the touchpad widget sensors highlighted when you touch it.

      **Figure 5. Widget view of the CAPSENSE&trade; tuner**

     <img src="images/widget-view.png" alt=""/>

7. You can view the raw count, baseline, difference count for each sensor and also the touchpad position in the **Graph View** tab. For example, to view the sensor data for a single sensor in Touchpad, select **Touchpad_Rx0_Tx0** under **Touchpad**.
       
   **Figure 6. Graph view of the CAPSENSE&trade; tuner**

   <img src="images/graph_view.png" alt=""/>

8. The **Touchpad View** tab shows the heat map view and the finger movement can be visualized on the same.

   **Figure 7. Touchpad view of the CAPSENSE&trade; Tuner**

   <img src="images/touchpad-view-tuner.png" alt=""/>

9. Observe the **Widget/Sensor Parameters** section in the CAPSENSE&trade; Tuner window. The compensation CDAC values for each touchpad sensor element calculated by the CAPSENSE&trade; resource is displayed as shown in **Figure 7**.

10. Verify that the SNR is greater than 5:1 by following the steps given in **Stage 5** [Tuning procedure](#tuning-procedure).

      The linearity of the position graph, non-reporting of false touches, and no discontinuity in the line drawing indicate a proper tuning.

11. The **Gesture View** tab visually represents evaluation and tuning of gestures (from one widget at a time).
The gesture view tab is disabled when there are no gesture widgets in the configuration.

      **Figure 8. Gesture view of the CAPSENSE&trade; Tuner**

      <img src="images/gesture-view-tuner.png" alt=""/>

12. **Gesture Monitor** provides visual indication for a detected gesture. **Gesture Event History** logs the detected gestures information.

      > **Note:** To open the Gesture Monitor window, Select **View** > **Gesture Monitor / Gesture Event History**

      **Figure 9. Gesture monitor view of the CAPSENSE&trade; Tuner**

      <img src="images/monitor-view-tuner.png" alt=""/>
      
</details>

<br>

## Tuning procedure

<details><summary><b> Create custom BSP for your board </b></summary>

1. Create a custom BSP for your board with any device by following the steps given in [ModusToolbox™ BSP Assistant user guide](https://www.infineon.com/ModusToolboxBSPAssistant). This code example was created for the device "CY8C4046LQI-T452".

2. Open the *design.modus* file from the *{Application root directory}/bsps/TARGET_APP_\<BSP-NAME>/config/* folder obtained in the previous step and enable CAPSENSE&trade; to get the *design.cycapsense* file. CAPSENSE&trade; configuration can then be started from scratch as explained below.
</details>

The following steps explain the tuning procedure. 

> **Note:** See the "Selecting CAPSENSE&trade; hardware parameters" section in the [PSoC&trade; 4 and PSoC&trade; 6 MCU CAPSENSE&trade; design guide](https://www.infineon.com/AN85951) to learn about the considerations for selecting each parameter values.

**Figure 10. CSX touchpad widget and Gesture tuning flow**

<img src="images/flowchart_for_tuning.png" alt="" width="600" />

Do the following to tune the touchpad widget:

<details> <summary><b>Stage 1: Set initial hardware parameters</b> </summary>

1. Connect the board to your PC using the provided USB cable through the KitProg3 USB connector.
2. Launch the device configurator tool.

   You can launch the device configurator in Eclipse IDE for ModusToolbox&trade; from the **Tools** section in the IDE Quick panel or in standalone mode from *{ModusToolbox&trade; install directory}/ModusToolbox/tools_{version}/device-configurator/device-configurator*. In this case, after opening the application, select **File** > **Open** and open the *design.modus* file of the respective application, which is present in the *{Application root directory}/bsps/TARGET_APP_\<BSP-NAME>/config/* folder.

3. In the [PSoC&trade; 4000T Kit](https://www.infineon.com/CY8CKIT-040T), the touchpad pins are connected to CAPSENSE&trade; channel (MSCLP 0). Therefore, make sure that you enable CAPSENSE&trade; channel in the Device Configurator, as shown in **Figure 11**.

   **Figure 11. Enable MSCLP channel in device configurator**

   <img src="images/device-configurator-channel.png" alt=""/>

      Save the changes and close the window.

4. Launch the CAPSENSE&trade; configurator tool.
   
   You can launch the CAPSENSE&trade; configurator tool in Eclipse IDE for ModusToolbox&trade; from the 'CAPSENSE&trade;' peripheral setting in the device configurator or directly from the **Tools** section in the IDE Quick panel. You can also launch it in standalone mode from *{ModusToolbox&trade; install directory}/ModusToolbox/tools_{version}/capsense-configurator/capsense-configurator*. In this case, after opening the application, select **File** > **Open** and open the *design.cycapsense* file of the respective application, which is present in the *{Application root directory}/bsps/TARGET_APP_\<BSP-NAME>/config/* folder.

   See the [ModusToolbox&trade; CAPSENSE&trade; configurator tool guide](https://www.infineon.com/ModusToolboxCapSenseConfig) for step-by-step instructions on how to configure and launch CAPSENSE&trade; in ModusToolbox&trade;. 

5. In the **Basic** tab, note that a touchpad **Touchpad** is configured with **CSX RM (Mutual-cap)** Sensing Mode.  

   **Figure 12. CAPSENSE&trade; configurator - Basic tab**

   <img src="images/capsense_basictab.png" alt=""/>

6. Do the following in the **General** tab under the **Advanced** tab:

   - Select **CAPSENSE&trade; IMO clock frequency** as 46 MHz.

   - Set **Modulator clock divider** to "1" to obtain the maximum available modulator clock frequency as recommended in the [PSoC&trade; 4 and PSoC&trade; 6 MCU CAPSENSE&trade; design guide](https://documentation.infineon.com/html/psoc6/epf1667481159393.html).

      > **Note:** The modulator clock frequency can be set to 46,000 kHz after changing the CAPSENSE&trade; IMO clock frequency to 46 MHz, because the modulator clock is derived from the CAPSENSE&trade; IMO clock. In the **CAPSENSE&trade; IMO clock frequency** drop-down list, select **46 MHz**. 

   - **Number of init sub-conversions** is set based on the hint shown when you hover over the edit box. Retain the default value. 
   
   - Because CIC2 filter is enabled, it is recommended to enable IIR filter. Retain the default settings for all filters. You can enable the filters later depending on the signal-to-noise ratio (SNR) requirements mentioned in **Stage 5**.
      
      Filters are used to reduce the peak-to-peak noise. Using filters will result in longer scan time.

   **Figure 13. CAPSENSE&trade; Configurator - General settings**

   <img src="images/adv_general.png" alt=""/>

   > **Note:** Each tab has a **Restore Defaults** button to restore the parameters of that tab to their default values.

7. Go to the **CSX Settings** tab and make the following changes:

   - Set **Inactive Sensor connection** to **Ground**.

   - Set **Number of reported fingers** to **2** for two-finger detection.

   - Select **Enable CDAC auto-calibration** and **Enable compensation CDAC**. 

      This helps in achieving the required CDAC calibration levels (40% of the maximum count) for all sensors in the widget, while maintaining the same sensitivity across the sensor elements.

   - Select **Enable CDAC dither**.

      This helps in removing flat-spots, by adding white noise that moves the conversion point around the flat-spots region.

   **Figure 14. CAPSENSE&trade; configurator - Advanced CSX settings**

   <img src="images/adv_csx.png" alt=""/>

8. Go to the **Widget Details** tab. Select **Touchpad** from the left pane, and then set the following:

   - **Maximum X-Axis position** and **Maximum Y-Axis position** to 255.

   - **Tx clock divider:** Retain default value (will be set in **Stage 3**)

   - **Clock source:** **Direct**

      **Note:** Spread spectrum clock (SSC) or PRS clock can be used as a clock source to deal with EMI/EMC issues.

   - **Number of sub-conversions:** 25

     25 is a good starting point to ensure a fast scan time and sufficient signal. This value will be adjusted as required in **Stage 4**. 

   - **Finger Threshold:** 20

     Finger Threshold is initially set to a low value, which allows the **Touchpad View** to track the finger movement during tuning.

   - **Noise Threshold:** 10

   - **Negative Noise Threshold:** 10 

   - **Hysteresis:** 5

   - **ON debounce:** 10

      These values reduces the influence of baseline on the sensor signal, which helps to get the true difference-count. Retain the default values for the widget threshold parameters; these parameters are set in **Stage 6**.
   
   - **Enable gestures:** **True**
       
      > **Note:** Select the Gestures you want to include in your application. In this CE, we are demonstrating the selected gestures shown in below figure.

   **Figure 15. CAPSENSE&trade; configurator - Widget details settings**

   <img src="images/adv_widget_detail.png" alt="" />

9. Go to the **Scan Configuration** tab to select the pins, the scan slots, and do the following:

   - Configure the pin for the electrode using the drop-down menu.

   - Configure the scan slot using the **Auto-Assign Slots** option or each sensor is allotted a scan slot based on the entered slot number. 

   - Check the notice list for warning or errors. 
   
      **Note:** Enable the **Notice List** in the **View** menu if it is not visible.

   **Figure 16. Scan configuration tab**

   <img src="images/scan-config.png" alt=""/>

10. Click **Save** to apply the settings.

</details>

<details><summary><b>Stage 2: Measure the sensor capacitance to set CDAC Dither parameter</b></summary>

The CAPSENSE&trade; middleware provides the built-in self-test (BIST) APIs to measure capacitances of sensors configured in the application. The sensor capacitances are referred to as  **C<sub>p</sub>** for CSD sensors and **C<sub>m</sub>** for CSX sensor.

Follow these steps to measure the C<sub>p</sub>/C<sub>m</sub> using BIST:

   1.	Open CAPSENSE™ Configurator from **Quick Panel** and enable the BIST library.

   **Figure 17. Enabling self test library**

   <img src="images/bist_measurement.png" alt="Figure 280" width=700>

   2.	Follow these steps to get the capacitance(C<sub>p</sub>/C<sub>m</sub>):
        - Add a breakpoint at the function call "measure_sensor_capacitance()" in *main.c*.
        - Run the application in debug mode.
        - Click the **Step over** button once break point hits.
        - Add an array variable sensor_capacitance to the **Expressions view** tab that holds the measured Cp values of configured sensors.

   **Figure 18. Measure C<sub>p</sub>/C<sub>m</sub> using BIST**

   <img src="images/debug-cp-measure.png" alt="Figure 280" width=700/>
   
   3.	The index of the sensor_capacitance array matches the sensor configuration in CAPSENSE&trade; Configurator, as shown in Figure 19.

   **Figure 19. Cp array index alignment**

   <img src="images/cp_alignment.png" alt="Figure 28" width=700/>

   

   4. For more details on BIST, See [CAPSENSE™ library and documents](https://github.com/Infineon/capsense).
   5. Keep this feature disabled in CAPSENSE&trade; Configurator, if not used in application.

### **CDAC Dither scale setting**
<br>

MSCLP uses CDAC dithering to reduce flat spots. Select the optimal dither scale parameter based on the sensor capacitance measured using BIST library.

See the following table for general recommended values of Dither scale.

**Table 1. Dither scale recommendation for CSD sensors**
 
Parasitic capacitance (C<sub>p</sub>) | Scale
:---: | :---:  
2pF <= C<sub>p</sub> < 3pF | 3
3pF <= C<sub>p</sub> < 5pF | 2
5pF <= C<sub>p</sub> < 10pF | 1
 C<sub>p</sub> >= 10pF  | 0

<br>

**Table 2. Dither Scale recommendation for CSX sensors**
 
Mutual capacitance (C<sub>m</sub>) | Scale
:---: | :---:  
300fF <= C<sub>m</sub> < 500fF | 5
500fF <= C<sub>m</sub> < 1000fF | 4
1000fF <= C<sub>m</sub> < 2000fF | 3
C<sub>m</sub> >= 2pF  | Follow [Table 1](#Table-1.-Dither-Scale-Recommendation-for-CSD-Sensors)

 Set the scale value in CAPSENSE&trade; Configurator as follows.

**Figure 20. CDAC Dither scale setting**

   <img src="images/dither-scale-value.png" alt="Figure 18" width=800/>

</details>

<details><summary><b>Stage 3: Set the sense clock frequency</b></summary>

The sense clock is derived from the modulator clock using a clock-divider and is used to scan the sensor by driving the CAPSENSE&trade; switched capacitor circuits. Both the clock source and clock divider are configurable. The sense clock divider should be configured such that the pulse width of the sense clock is long enough to allow the sensor capacitance to charge and discharge completely. This is verified by observing the charging and discharging waveforms of the sensor using an oscilloscope and an active probe. The sensors should be probed close to the electrode and not at the sense pins or the series resistor. 

See [Figure 21](#figure-21-proper-charge-cycle-of-a-sensor) and [Figure 22](#figure-22-improper-charge-cycle-of-a-sensor) for waveforms observed on the shield. [Figure 21](#figure-21-proper-charge-cycle-of-a-sensor) shows proper charging when the sense clock frequency is correctly tuned. The pulse width is at least 5 Tau, i.e., the voltage is reaching at least 99.3% of the required voltage at the end of each phase. [Figure 22](#figure-22-improper-charge-cycle-of-a-sensor) shows incomplete settling (charging/discharging).


##### **Figure 21. Proper charge cycle of a sensor**

<img src="images/csdrm-waveform.png" alt="Figure 19" width="600"/>

<br>

##### **Figure 22. Improper charge cycle of a sensor**

<img src="images/csdrm-waveform-improper.png" alt="Figure 20" width="600"/>

1. Program the board and launch CAPSENSE&trade; Tuner.

2. See the charging waveform of the sensor as described earlier. 

3. If the charging is incomplete, increase the sense clock divider. This can be done in CAPSENSE&trade; Tuner by selecting the Sensor and editing the **Sense Clock Divider** parameter in the Widget/Sensor Parameters panel.

  > **Note:** The sense clock divider should be **divisible by 2**. This ensures that both the scan phases have equal durations. 

   After editing the value, click the **Apply to Device** button and observe the waveform again. Repeat this until complete settling is observed.  
   
4. Click the Apply to Project button so that the configuration is saved to your project. 

   **Figure 23. Sense Clock Divider setting**

   <img src="images/sense_clock_divider_setting.png" alt="Figure 21" />
   

5. Repeat this process for all the sensors and the Shield. Each sensor may require a different sense clock divider value to charge/discharge completely. But all the sensors that are in the same scan slot need to have the same sense clock source, sense clock divider, and number of sub-conversions. Therefore, take the largest sense clock divider in a given scan slot and apply it to all the other sensors that share that slot.

</details>

<details> <summary><b> Stage 4: Obtain crossover point and noise</b> </summary>

1. Program the board.

2. Launch the CAPSENSE&trade; Tuner to monitor the CAPSENSE&trade; data and for CAPSENSE&trade; parameter tuning and SNR measurement.

   See the [CAPSENSE&trade; Tuner guide](https://www.infineon.com/ModusToolboxCapSenseTune) for step-by-step instructions on how to launch and configure the CAPSENSE&trade; Tuner in ModusToolbox&trade; software.
     
3. Capture the raw counts of each sensor element in the touchpad (as shown in **Figure 24**) and verify that they are approximately (± 5%) equal to 40% of the MaxCount. See [design guide](https://www.infineon.com/AN85951) for the MaxCount equation.

   1. Go to the **Touchpad View** tab and change the **Display settings** as follows:

      - **Data type:** RawCount

      - **Value type:** Current

      - **Number of samples:** 1000

    **Figure 24. Raw counts obtained on the Touchpad View tab in the tuner window**

     <img src="images/touchpad-view-rc.png" alt="" />

4. Capture and note the peak-to-peak noise of each sensor element in the touchpad.

   1. From the **Widget Explorer** section, select the  **Touchpad** widget.

   2. Go to the **Touchpad View** tab and change the **Display settings** as follows:

      - **Display mode:** Touch Reporting

      - **Data type:** RawCount

      - **Value type:** Max-Min

      - **Number of Samples:** 1000

      Capture the variation in the raw counts for 1000 samples, without placing a finger (which gives the peak-to-peak noise) and note the highest noise.

     > **Note:** Under **Widget selection**, enable **Swap XY-axes** for proper visualization of finger movement on the touchpad.

      **Figure 25. Noise obtained on the Touchpad View tab in the tuner window**

      <img src="images/touchpad-view-noise.png" alt="" />

      **Table 3. Max peak-to-peak noise obtained in CY8CKIT-040T**

      |Kit | Max peak-to-peak noise|
      |:----------|:-------------------------|
      |CY8CKIT-040T   |173|

7. A finger (6 mm) should be held on the touchpad in the least touch intensity (LTI) position (at the intersection of four nodes) as shown in the following figure.

   **Figure 26. Least touch intensity (LTI) position**

   <img src="images/lti-position.png" alt="" width="100" />

   **Note:** Finger movement during the test can artificially increase the noise level.

   1. Go to the **Touchpad View** tab and change the **Display settings** as follows:

      - **Display mode:** Touch Reporting

      - **Data type:** DiffCount

      - **Value type:** Current

   2. Place the finger such that an almost equal signal is obtained in all four intersecting nodes (look at the heat map displayed in the **Touchpad View** tab as shown in **Figure 27**).

      **Note:** The LTI signal is measured at the farthest point of the touchpad from the sensor pin connection, where the sensors have the worst-case RC-time constant.

      **Figure 27. LTI position in touchpad view**

      <img src="images/touchpad-view-lti.png" alt="" />

      LTI Signal = (1145 + 1060 + 1114 + 1183)/4 = 1125

</details>

<details> <summary><b> Stage 5. Fine-tune sensitivity for 5:1 SNR</b> </summary>
----------------------

The CAPSENSE&trade; system may be required to work reliably in adverse conditions such as a noisy environment. The touchpad sensors should be tuned with SNR > 5:1 to avoid triggering false touches and to make sure that all intended touches are registered in these adverse conditions.

> **Note:** For gesture detection, it is recommended to have approximately 10:1 SNR.

1. Ensure that the LTI Signal count is greater than 50 and meets at least 5:1 SNR (using **Equation 1**).

   In the **CAPSENSE&trade; Tuner** window, increase the **Number of sub-conversions** (located in the **Widget/Sensor Parameters** section, under **Widget Hardware Parameters**) by 10 until you achieve this requirement.

   **Equation 1: Measuring the SNR**

   ![](images/snr-equation.png)

   Where,

   - LTI signal is the signal obtained as shown in **Figure 27**

   - Pk-Pk noise is the peak-to-peak noise obtained as shown in **Figure 25**

   SNR is measured using **Equation 1**.

   Here, from **Figure 25** and **Figure 27**,

   SNR = 1125/173 = **6.5**

   **Note:** Ensure that the **Number of sub-conversions** (Nsub) does not exceed the max limit and saturate the raw count.

2. Update the number of sub-conversions

   - Update the number of sub-conversions (Nsub) directly in the **Widget/Sensor parameters** tab of the CAPSENSE&trade; tuner.

   - CY8CKIT-040T has an in-built CIC2 filter which increases the resolution for the same scan time, see [AN234231 - Achieving lowest-power capacitive sensing with PSoC&trade; 4000T](https://www.infineon.com/AN234231) for detailed information on CIC2 filter.

   - Current consumption is directly proportional to number of sub-conversion, therefore decrease the number of sub-conversions to achieve lower current consumption.

     > **Note:** Number of sub-conversion should be greater than or equal to 8.

   - Calculate decimation rate using **Equation 2**. Resolution increases with increase in decimation rate, therefore set the maximum decimation rate.

      **Equation 2. Decimation rate**

      ![](images/decimation-equation.png)

     > **Note:** Decimation rate should not exceed 255.

3. After changing the **Number of sub-conversions**, click **Apply to Device** to send the setting to the device. The change is reflected in the graphs.

  > **Note:** The **Apply to Device** option is enabled only when the **Number of sub-conversions** is changed.

4. If the SNR condition is not achieved even with the maximum number of sub-conversions, enable filters in the **General** settings (go to the **Advanced** tab of the CAPSENSE&trade; configurator). This is generally not required for this kit.
</details>

<details> <summary><b>Stage 6: Tune threshold parameters</b> </summary>

After confirming that your design meets the timing parameters and power requirements, and the SNR is greater than 5:1, set your threshold parameters.

> **Note:** Thresholds are set based on the LTI position, because it is the least valid touch signal that can be obtained.

Set the recommended threshold values for the Touchpad widget using the LTI signal value obtained in **Stage 5**:

   - **Finger Threshold:** 80% of the LTI signal

   - **Noise Threshold:** Twice the highest noise or 40% of the LTI signal (whichever is greater)

   - **Negative Noise Threshold:** Twice the highest noise or 40% of the LTI signal (whichever is greater)

   - **Hysteresis**

      Do the following:

      1. Place the finger in the LTI position.

      2. Set the **Data type** to DiffCount and **Value type** to Max-Min in the **Touchpad View** tab and click **Clear**.

      3. Record the max-min count value (Max_Min_count) of the selected 2x2 sensors.

         **Figure 28. Obtaining the hysteresis**

         <img src="images/touchpad-view-hys.png" alt="" width="1000" />

      4. Hysteresis = Max_Min_count/2 = 215/2 = 107

   - **ON Debounce:**  10 (Set to 1 for gesture detection)

   - **Low Baseline Reset:** Default value of 30

   - **Velocity:** Default value of 2500

     > **Note:** For multiple finger detection, if the velocity value is low, two touches at different positions are considered to be two different finger touches. On the other hand, if it is set at a higher value, it is considered to be the same finger moving to a different position.

   **Table 4. Software tuning parameters obtained for CY8CKIT-040T**

   |Parameter|	CY8CKIT-040T |
   |:--------|:------|
   |Number of Sub-conversions	| 180 |
   |Finger threshold 	| 900 |
   |Noise threshold | 450 |
   |Negative noise threshold	| 450 |
   |Low baseline reset	| 30 |
   |Hysteresis	| 107 |
   |ON debounce	| 10 |
   |Velocity| 2500 |

</details>

<details><summary><b> Stage 7: Set gesture parameters</b></summary>

You can set the gesture parameters directly in the **Widget/Sensor parameters** tab of the CAPSENSE&trade; tuner and observe the results in the Gesture Monitor/Gesture View .

> **Note:** Click on the parameter to understand the definition and its valid range .

   **Figure 29. Gesture parameters**

   <img src="images/gesture_parameters.png" alt="" width="500" />

In this application gesture parameters have been set for the typical use case, but user can change these parameters as per the need of their application use case. 


#### **Apply settings to firmware**

1. Click **Apply to Device** and **Apply to Project** in the CAPSENSE&trade; Tuner window to apply the settings to the device and project, respectively. Close the tuner.

   **Figure 30. Apply to Project**

   <img src="images/apply_to_project.png" alt="" width="500" />


</details>

<br>

## Debugging

You can debug the example to step through the code. In the IDE, use the **\<Application Name> Debug (KitProg3_MiniProg4)** configuration in the **Quick Panel**. For details, see the "Program and debug" section in the [Eclipse IDE for ModusToolbox&trade; software user guide](https://www.infineon.com/MTBEclipseIDEUserGuide).


## Design and implementation

The project contains a touchpad widget configured in CSX-RM Sensing Mode. See the [Tuning procedure](#tuning-procedure) section for step-by-step instructions to configure the other settings of the **CAPSENSE&trade; configurator**.

The project uses the [CAPSENSE&trade; middleware](https://github.com/Infineon/capsense) (see ModusToolbox&trade; user guide for more details on selecting a middleware). See [AN85951 – PSoC&trade; 4 and PSoC&trade; 6 MCU CAPSENSE&trade; design guide](https://www.infineon.com/AN85951) for more details on CAPSENSE&trade; features and usage.

The [ModusToolbox&trade;](https://www.infineon.com/modustoolbox) provides a GUI-based tuner application for debugging and tuning the CAPSENSE&trade; system. The CAPSENSE&trade; Tuner application works with EZI2C and UART communication interfaces. This project has an SCB block configured in EZI2C mode to establish communication with the onboard KitProg, which in turn enables reading the CAPSENSE&trade; raw data by the CAPSENSE&trade; Tuner; see Figure 32.

The CAPSENSE&trade; data structure that contains the CAPSENSE&trade; raw data is exposed to the CAPSENSE&trade; tuner by setting up the I2C communication data buffer with the CAPSENSE&trade; data structure. This enables the tuner to access the CAPSENSE&trade; raw data for tuning and debugging CAPSENSE&trade;.

The successful tuning of the touchpad is indicated by the RGB LED in the evaluation kit; the LED1 brightness increases when finger is moved from bottom to up  and LED3 brightness increases when finger is moved from left to right on the touchpad.

The MOSI pin of the SPI slave peripheral is used to transfer data to the three serially connected LEDs for controlling color, brightness, and ON or OFF operation. The three LEDs form a daisy-chain connection and the communication happens over the serial interface to create an RGB configuration. The LED accepts a 32-bit input code, with three bytes for red, green, and blue color, five bits for global brightness, and three blank ‘1’ bits. See the [LED datasheet](https://media.digikey.com/pdf/Data%20Sheets/Everlight%20PDFs/12-23C_RSGHBHW-5V01_2C_Rev4_12-17-18.pdf) for more details.

### Steps to set up the VDDA supply voltage in device configurator

1. Open Device configurator from the Quick panel. 

2. Go to the **Systems** tab, select the **Power** resource, and set the VDDA value under **Operating Conditions** as shown in **Figure 31**.

   **Figure 31. Setting the VDDA supply in the system tab of device configurator**

   <img src="images/vdda-settings.png" alt="" width="800"/>

### Resources and settings

See the [Operation](#operation) section for step-by-step instructions to configure the CAPSENSE&trade; configurator.

**Figure 32. Device configurator - EZI2C peripheral parameters**

<img src="images/ezi2c_config.png" alt="" width="600"/>

**Figure 33. SPI settings**

<img src="images/spi-settings.png" alt="" width="600"/>

**Table 5. Application resources**



| Resource  |  Alias/object     |    Purpose     |
| :------- | :------------    | :------------ |
| SCB (I2C) (PDL) | CYBSP_EZI2C          | EZI2C slave driver to communicate with CAPSENSE&trade; tuner GUI |
| CAPSENSE&trade; | CYBSP_MSCLP0 | CAPSENSE&trade; driver to interact with the MSCLP hardware and interface the CAPSENSE&trade; sensors |
| Digital pin | CYBSP_USER_LED | To visualise the touchpad response |

### Firmware flow

**Figure 34. Firmware flowchart**

<img src="images/firmware_flow.png" alt="" width="400"/>

## Related resources

Resources  | Links
-----------|----------------------------------
Application notes  | [AN79953](https://www.infineon.com/AN79953) – Getting started with PSoC&trade; 4 <br> [AN85951](https://www.infineon.com/AN85951) – PSoC&trade; 4 and PSoC&trade; 6 MCU CAPSENSE&trade; design guide <br> AN234231 - Achieving lowest-power capacitive sensing with PSoC&trade; 4000T
Code examples | [Using ModusToolbox&trade; software](https://github.com/Infineon/Code-Examples-for-ModusToolbox-Software) on GitHub <br> [Using PSoC&trade; Creator](https://www.infineon.com/cms/en/design-support/software/code-examples/psoc-3-4-5-code-examples-for-psoc-creator)
Device documentation | [PSoC&trade; 4 datasheets](https://www.infineon.com/cms/en/search.html?intc=searchkwr-return#!view=downloads&term=psoc%204&doc_group=Data%20Sheet) <br>[PSoC&trade; 4 technical reference manuals](https://www.infineon.com/cms/en/search.html#!term=psoc%204%20technical%20reference%20manual&view=all)
Development kits | Select your kits from the [Evaluation board finder](https://www.infineon.com/cms/en/design-support/finder-selection-tools/product-finder/evaluation-board)
Libraries on GitHub  | [mtb-hal-cat2](https://github.com/Infineon/mtb-hal-cat2) – Hardware Abstraction Layer (HAL) library
Middleware on GitHub | [capsense](https://github.com/Infineon/capsense) – CAPSENSE&trade; library and documents <br>
Tools | [Eclipse IDE for ModusToolbox&trade;](https://www.infineon.com/modustoolbox) – ModusToolbox&trade; software is a collection of easy-to-use software and tools enabling rapid development with Infineon MCUs, covering applications from embedded sense and control to wireless and cloud-connected systems using AIROC&trade; Wi-Fi and Bluetooth&reg; connectivity devices. <br> [PSoC&trade; Creator](https://www.infineon.com/cms/en/design-support/tools/sdk/psoc-software/psoc-creator/) – IDE for PSoC&trade; and FM0+ MCU development

<br>

## Other resources

Infineon provides a wealth of data at www.infineon.com to help you select the right device, and quickly and effectively integrate it into your design.

## Document history

Document title: *CE235339* - *PSoC&trade; 4: MSCLP multi-touch mutual-capacitance touchpad tuning*

 Version | Description of change
 ------- | ---------------------
 1.0.0   | New code example. <br /> This version is not backward compatible with ModusToolbox&trade; software v2.4.
 1.0.1   | Project dependency update. 
 1.1.0   | Minor folder structure changes that doesn't break backward compatibility.
 1.2.0   | Minor README and configuration update.
 2.0.0   | Major update to support ModusToolbox™ software v3.1 This version is not backward compatible with ModusToolbox™ software v3.0.
 2.1.0   | Gesture demonstration added on a mutual-capacitance-based touchpad widget. 



All other trademarks or registered trademarks referenced herein are the property of their respective owners.

---------------------------------------------------------

© Cypress Semiconductor Corporation, 2023. This document is the property of Cypress Semiconductor Corporation, an Infineon Technologies company, and its affiliates ("Cypress").  This document, including any software or firmware included or referenced in this document ("Software"), is owned by Cypress under the intellectual property laws and treaties of the United States and other countries worldwide.  Cypress reserves all rights under such laws and treaties and does not, except as specifically stated in this paragraph, grant any license under its patents, copyrights, trademarks, or other intellectual property rights.  If the Software is not accompanied by a license agreement and you do not otherwise have a written agreement with Cypress governing the use of the Software, then Cypress hereby grants you a personal, non-exclusive, nontransferable license (without the right to sublicense) (1) under its copyright rights in the Software (a) for Software provided in source code form, to modify and reproduce the Software solely for use with Cypress hardware products, only internally within your organization, and (b) to distribute the Software in binary code form externally to end users (either directly or indirectly through resellers and distributors), solely for use on Cypress hardware product units, and (2) under those claims of Cypress’s patents that are infringed by the Software (as provided by Cypress, unmodified) to make, use, distribute, and import the Software solely for use with Cypress hardware products.  Any other use, reproduction, modification, translation, or compilation of the Software is prohibited.
<br>
TO THE EXTENT PERMITTED BY APPLICABLE LAW, CYPRESS MAKES NO WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, WITH REGARD TO THIS DOCUMENT OR ANY SOFTWARE OR ACCOMPANYING HARDWARE, INCLUDING, BUT NOT LIMITED TO, THE IMPLIED WARRANTIES OF MERCHANTABILITY AND FITNESS FOR A PARTICULAR PURPOSE.  No computing device can be absolutely secure.  Therefore, despite security measures implemented in Cypress hardware or software products, Cypress shall have no liability arising out of any security breach, such as unauthorized access to or use of a Cypress product. CYPRESS DOES NOT REPRESENT, WARRANT, OR GUARANTEE THAT CYPRESS PRODUCTS, OR SYSTEMS CREATED USING CYPRESS PRODUCTS, WILL BE FREE FROM CORRUPTION, ATTACK, VIRUSES, INTERFERENCE, HACKING, DATA LOSS OR THEFT, OR OTHER SECURITY INTRUSION (collectively, "Security Breach").  Cypress disclaims any liability relating to any Security Breach, and you shall and hereby do release Cypress from any claim, damage, or other liability arising from any Security Breach.  In addition, the products described in these materials may contain design defects or errors known as errata which may cause the product to deviate from published specifications. To the extent permitted by applicable law, Cypress reserves the right to make changes to this document without further notice. Cypress does not assume any liability arising out of the application or use of any product or circuit described in this document. Any information provided in this document, including any sample design information or programming code, is provided only for reference purposes.  It is the responsibility of the user of this document to properly design, program, and test the functionality and safety of any application made of this information and any resulting product.  "High-Risk Device" means any device or system whose failure could cause personal injury, death, or property damage.  Examples of High-Risk Devices are weapons, nuclear installations, surgical implants, and other medical devices.  "Critical Component" means any component of a High-Risk Device whose failure to perform can be reasonably expected to cause, directly or indirectly, the failure of the High-Risk Device, or to affect its safety or effectiveness.  Cypress is not liable, in whole or in part, and you shall and hereby do release Cypress from any claim, damage, or other liability arising from any use of a Cypress product as a Critical Component in a High-Risk Device. You shall indemnify and hold Cypress, including its affiliates, and its directors, officers, employees, agents, distributors, and assigns harmless from and against all claims, costs, damages, and expenses, arising out of any claim, including claims for product liability, personal injury or death, or property damage arising from any use of a Cypress product as a Critical Component in a High-Risk Device. Cypress products are not intended or authorized for use as a Critical Component in any High-Risk Device except to the limited extent that (i) Cypress's published data sheet for the product explicitly states Cypress has qualified the product for use in a specific High-Risk Device, or (ii) Cypress has given you advance written authorization to use the product as a Critical Component in the specific High-Risk Device and you have signed a separate indemnification agreement.
<br>
Cypress, the Cypress logo, and combinations thereof, ModusToolbox, PSoC, CAPSENSE, EZ-USB, F-RAM, and TRAVEO are trademarks or registered trademarks of Cypress or a subsidiary of Cypress in the United States or in other countries. For a more complete list of Cypress trademarks, visit www.infineon.com. Other names and brands may be claimed as property of their respective owners.
