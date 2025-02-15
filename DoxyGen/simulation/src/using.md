\page Using Using Arm Fixed Virtual Platforms

This section describes how to use the **Arm Fixed Virtual Platforms (FVPs)**.

The FVP simulation models in AVH context correspond to the [Arm Fast Models Fixed Virtual Platforms](https://developer.arm.com/tools-and-software/simulation-models/fixed-virtual-platforms) with extensions for \ref arm_cmvp. The table below shows the available models:

FVP Simulation Model           | Processor Core        | Overview Description
:------------------------------|:----------------------|:----------------------------------------
VHT_MPS2_Cortex-M0             | Cortex-M0             | [ARM Cortex-M0 SMM on V2M-MPS2 (AppNote AN382)](https://developer.arm.com/documentation/dai0382)
VHT_MPS2_Cortex-M0plus         | Cortex-M0+            | [ARM Cortex-M0+ SMM on V2M-MPS2 (AppNote AN383)](https://developer.arm.com/documentation/dai0383)
VHT_MPS2_Cortex-M3             | Cortex-M3             | [ARM Cortex-M3 SMM on V2M-MPS2 (AppNote AN385)](https://developer.arm.com/documentation/dai0385)
VHT_MPS2_Cortex-M4             | Cortex-M4             | [ARM Cortex-M4 SMM on V2M-MPS2 (AppNote AN386)](https://developer.arm.com/documentation/dai0386)
VHT_MPS2_Cortex-M7             | Cortex-M7             | [ARM Cortex-M7 SMM on V2M-MPS2 (AppNote AN399)](https://developer.arm.com/documentation/dai0386)
VHT_MPS2_Cortex-M23            | Cortex-M23            | [ARM Cortex-M23 IoT Subsystem for V2M-MPS2+ (AppNote AN519)](https://developer.arm.com/documentation/dai0519)
VHT_MPS2_Cortex-M33            | Cortex-M33            | [ARM Cortex-M33 IoT Subsystem for V2M-MPS2+ (AppNote AN505)](https://developer.arm.com/documentation/dai0505)
VHT_MPS3_Corstone_SSE-300      | Cortex-M55            | [Corstone-300 FVP Technical Overview (PDF)](./Corstone_SSE-300_Ethos-U55_FVP_MPS3_Technical_Overview.pdf),  [Memory map overview](https://developer.arm.com/documentation/100966/1118/Arm--Corstone-SSE-300-FVP/Memory-map-overview-for-Corstone-SSE-300)
VHT_Corstone_SSE-300_Ethos-U55 | Cortex-M55, Ethos-U55 | [Corstone-300 FVP Technical Overview (PDF)](./Corstone_SSE-300_Ethos-U55_FVP_MPS3_Technical_Overview.pdf),  [Memory map overview](https://developer.arm.com/documentation/100966/1118/Arm--Corstone-SSE-300-FVP/Memory-map-overview-for-Corstone-SSE-300)
VHT_Corstone_SSE-300_Ethos-U65 | Cortex-M55, Ethos-U65 | [Corstone-300 FVP Technical Overview (PDF)](./Corstone_SSE-300_Ethos-U55_FVP_MPS3_Technical_Overview.pdf),  [Memory map overview](https://developer.arm.com/documentation/100966/1118/Arm--Corstone-SSE-300-FVP/Memory-map-overview-for-Corstone-SSE-300)
VHT_Corstone_SSE-310           | Cortex-M85, Ethos-U55 | [Corstone-310 FVP Technical Overview (PDF)](./Corstone_SSE-310_FVP_Technical_Overview.pdf),  [Memory map overview](https://developer.arm.com/documentation/100966/1118/Arm--Corstone-SSE-310-FVP/Corstone-SSE-310-FVP-memory-map-overview)
VHT_Corstone_SSE-310_Ethos-U65 | Cortex-M85, Ethos-U65 | [Corstone-310 FVP Technical Overview (PDF)](./Corstone_SSE-310_FVP_Technical_Overview.pdf),  [Memory map overview](https://developer.arm.com/documentation/100966/1118/Arm--Corstone-SSE-310-FVP/Corstone-SSE-310-FVP-memory-map-overview)

Additionally following FVP models are provided without support of Virtual Peripherals:

Simulation Model               | Processor Core        | Overview Description
:------------------------------|:----------------------|:----------------------------------------
FVP_Corstone-1000              | Cortex-A35, Cortex-M0+, Cortex-M3 | [Arm Corstone-1000 for MPS3 (AppNote AN550)](https://developer.arm.com/documentation/dai0550/)

# Execution {#Execution}

FVP models can be executed in Linux environment by using their model names, for example `VHT_Corestone_SSE-300_Ethos-U55`, and on Windows platform the models are provided as executables files, for example `VHT_Corestone_SSE-300_Ethos-U55.exe`. See \ref Example.

# Command Line Options {#Options}

The command line options can be listed using the -help command. For example in Linux environment:

```
VHT_Corstone_SSE-300_Ethos-U55 -help
```

The FVP models can be configured using the option *-f FILE* that specifies a *config-file*. The available *config-file* options can be listed with the option *-l*.

# Usage Examples {#Example}

Below is an example of running a program on the AVH model for Corstone-300 with Ethos-U55 in Linux environment:

```
VHT_Corstone_SSE-300_Ethos-U55 -V "..\VSI\audio\python" -f vht_config.txt -a Objects\microspeech.axf --stat --simlimit 24
```

Where:
  - **-V** specifies that path to the Python scripts for \ref arm_cmvp.
  - **-f** specifies the *config-file* for the AVH simulation model.
  - **-a** specifies the application to load.
  - **--stat** instructs to print run statistics on simulation exit.
  - **--simlimit** specifies the maximum number of seconds to simulate.

The content of the *vht_config.txt* could be:
```
# Parameters:
# instance.parameter=value       #(type, mode) default = 'def value' : description : [min..max]
#------------------------------------------------------------------------------
core_clk.mul=32000000                                 # (int   , init-time) default = '0x17d7840' : Clock Rate Multiplier. This parameter is not exposed via CADI and can only be set in LISA
mps3_board.telnetterminal0.start_telnet=0             # (bool  , init-time) default = '1'      : Start telnet if nothing connected
mps3_board.uart0.out_file=-                           # (string, init-time) default = ''       : Output file to hold data written by the UART (use '-' to send all output to stdout)
mps3_board.visualisation.disable-visualisation=1      # (bool  , init-time) default = '0'      : Enable/disable visualisation
#------------------------------------------------------------------------------
```

Where:
 - **core_clk.mul=32000000** specifies the virtual time, in this case 32MHz CPU clock.
 - **mps3_board.telnetterminal0.start_telnet=0** disables the Telnet connectivity.
 - **mps3_board.uart0.out_file=-** UART output is send to stdout.
 - **mps3_board.visualisation.disable-visualisation=1** disables the graphical user interface of the AVH.

## Execution stop

Embedded applications typically run with an infinite loop that ensures continuous program execution. But for executing regression tests as part of Continuous Integration (CI) workflows it is often required that program execution is stopped after a test is completed, so that the next test can be started.

FVP models have `shutdown_on_eot` parameter that enables simple implementation of such program exit. The parameter should be set in the model configuration file (*vht_config.txt* explained above), for example for VHT_Corstone_SSE-300:

```
mps3_board.uart0.shutdown_on_eot=1   # (bool, init-time) default = '0' : Shutdown simulation when a EOT (ASCII 4) char is transmitted (useful for regression tests when semihosting is not available)
```

And then to trigger the shutdown, a EOT (ASCII 4) symbol can be transmitted to the corresponding serial interface from the program. The code below demonstrates an example, where the execution is stopped after target execution count is achieved. In this implementation the STDIO is assumed to be retargeted to the UART0:

```
  while (1)  {
    printf ("Hello World %d\r\n", count);
    if (count > 100) printf ("\x04");  // EOT (0x04) stops simulation
    count++;
    osDelay (1000);
  }
```
