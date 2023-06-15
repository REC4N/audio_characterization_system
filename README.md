# Audio characterization system
The objective of this project is to create an embedded system that can change the “essence” of a audio signal, as if it is played on a specific room or environment. The biggest advantage of this system is that it allows for recording and playback on any environment, and it is cheaper than commercial alternatives.

## List of materials
To recreate this project, the following components are required:
- TUL PYNQ™-Z2 board
- Microphone that is capable of recording at 44.1 kHz
- Ethernet cable connected between the embedded system and PC.
- Speakers to be able to listen the audio samples.

## Where to start?
This project leverages the computing power of the Zynq Soc, by using both Python running on an ARM Cortex processor and an FPGA fabric directly connected to it. The main program, `audio_characterization_main.ipynb`, showcases an example of using an input audio signal and processing it with the sound characteristics of a stairwell. The input sound was `cello.wav`, the environment is characterized by the impulse response of the stairwell `stairs_impulse`, and the output of the system is `processed_audio_16bit.wav`. These wav files has been provided for a quick demonstration of the power of the system. It is possible to use any new wav files for the input signal or environment filter. It is also possible to record them locally!

Part of the processing power was offloaded to the FPGA fabric. The system leverages the PYNQ platform to use Python to transfer data into the FPGA fabric for quick processing of information. For this version of the project, low pass filtering (used as intermediate stages for downsampling and upsampling of data) was done completely on the FPGA. The _Vivado_ folder contains all the files and code used to create the hardware required to transfer data between DRAM, the FPGA fabric, and the filter. If deep inspection of the architecture is desired, run the following command on the TCL window of Vivado to reconstruct the project on your local machine: `source generateSystemProject.tcl` (be sure to change directory first to where the file _generateSystemProject.tcl_ was cloned). The PYNQ platform requires the bitstream file, hardware file and tcl script to be able to synthesize the desired architecture into the FPGA at runtime of the Python program. These three files were also provided for ease of use in the `PYNQ_overlay_files` folder. If any changes are done to the architecture, generating a new bitstream is required. Refer to the `Documentation` to see in depth how to do this and where this files are placed in the system. The script `LPF_FPGA_Verification.ipynb` demonstrates correct functionality of the low pass filter in the FPGA. 

To run `audio_characterization_main.ipynb`, check for the following:
- Use a PYNQ image of V3 or above.
- Install the package `soundfile` into the Pynq system by running `sudo pip3 install soundfile` on the bash shell.
- Move the contents of `PYNQ_overlay_files` into `\pynq\xilinx\pynq\overlays` directory on the embedded system. The notebook uses the following path for the bitstream file: `/home/xilinx/pynq/overlays/LPF/low_pass_filter.bit`. The rest of the files from  `PYNQ_overlay_files` are on the same directory.

## How can I change the input signal and environment filter files?
The `audio_characterization_main.ipynb` showcases how to do it, by either using pre-recorded wav files, or record new ones.

## Questions?
`Documentation` contains information regarding how the system works, and how to modify it. 


