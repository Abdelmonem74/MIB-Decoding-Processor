1- PHY.jpg 
MIB decoding Processor: contains 3 main sub-systems (256-Point FFT sub-system, Channel Est./Eq. sub-system and Decoder sub-system). It also includes Register-Interface (RIF) to communicate with the CPU.

My sub-system is the one between FFT and Decoder (we called it Post-FFT subsystem). 
It is responsible for converting each received OFDM symbol (consisting of 256-subcarriers) to the transmitted version of it. 
In other words, we resolve the channel impact to recover the correct transmitted signal.
This is done by estimating the channel after the FFT (In frequency domain).

The question is how do we estimate the channel?
In wireless communications, The Tx and Rx agree on inserting some known-data to both of them (called Pilots) between the actual data , they are responsible for estimating the channel at their sub-carriers.
but we want to estimate the channel at the actual data subcarriers to recover the original data! We can do interpolation (linear or Sinc) or we can use MMSE which is much better (observe BER.jpg).

2- PostFFT Interfaces.PDF
PostFFT sub-system interface with the RIF to read some parameters such as cell-ID number, i_SSB and Half-frame; those parameters are given to our system from the synchronization phase which we assume is done before we start.
PostFFT sub-system interface with the coefficient memory which are pre-computed by the CPU and depend on the number of channel Taps.
PostFFT sub-system interface with FFT memory to read the received data (DMRS & PBCH).
PostFFT sub-system interface with Decoder memory to write the generated Log Likelihood data (LLRs).
PostFFT sub-system interface with the TOP controller.


3- Post-FFT.jpg
Note : 	DMRS-> De-modulation reference signals which are the pilots.
	PBCH-> Physical broadcast channel data which is the actual data we want to recover.
The Post-FFT sub-system consists of the Channel Estimation block, Channel Equalizer block as well as some Bit-Processing blocks.

4- ChEst.jpg | Channel Estimation block
Consists of 	Least-Square Estimator : estimate the channel at the DMRS subcarriers.
		Minimum Mean Square Estimator : estimate the channel everywhere.
		TX-DMRS generator : generate the known pilots.
		Memory wrapper : some MUXes to control the memory write/read operations.
		Channel Average : It averages the estimates of three OFDM symbols into one (assume time invariant channel). 

5- Bit-Processing.jpg
It scrambles, interleaves and selects some of the data to resolve the impact of these blocks at the transmitter side.
