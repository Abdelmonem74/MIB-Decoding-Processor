# MIB-Decoding-Processor
MIB decoding Processor is basically the full decoding chain for the Physical Broadcast Channel (PBCH) that carries the important Master Information Block (MIB). 
The PBCH Decoding processor is a purely digital processor that is customized to decode the PBCH channel within the NR modem. 
Form the overall system perspective and the microprocessor point-of-view, this processor is employed as a HW accelerator that receives a command from the microprocessor through its register interface. 
The command is mainly to decode the PBCH channel. However, this command should be associated with various system parameters (such as the cell ID, the time stamp, … etc) that enables the PBCH Decoding processor to decode the PBCH. 
In return, the PBCH Decoding processor would inform the microprocessor that the processing is complete through an interrupt system and/or a register polling mechanism. 
The PBCH Decoding processor would save the results in some internal registers that are accessible through the register interface. 
The results are mainly the MIB payload if the PBCH is decoded successfully, and an indicator whether the PBCH is decoded successfully or not.
The PBCH Decoding processor implements the typical receiver chain for the PBCH detection. 
This processor has some mandatory building blocks including the FFT, channel estimation and equalization, demodulation process, and the channel decoding stage. 
One important feature about this processor is its ability to control the various building blocks within the blind decode trials.
