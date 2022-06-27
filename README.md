# TODO: finish this section with all the config file parameters

# The Windows branch
This is a minimal version of rsudp with only the relevant modules and dependencies for the use case of small ground vibration disturbance detection, ready for production deployment in windows OS.

## Installation instruction

 

## How to start the program



# Configuration File Parameters
## settings:
- **station**: OFFLN  --> trigger use of offline inventory file (in inventory_files folder) for deconvolution (does not attempt to download it from the server)
- **scaling_sensitivity**: sensitivity of the geophone. This parameter is used to compute velocity [$m/s$] from the AD-converter voltage counts. It is only used in modules where the *manual_scaling* option is set to true. Default value: 250000000 [$counts/(m/s)$]. It provides and alternative to the built-in obspy deconvolution module. 
- **db_reference**: reference velocity value to compute dB intensity. Default value: 1 $\mu m/s$ (1e-6).

## plot:
This is the standard plotting module from rsudp extended to enable displaying of intensity(dB) as well as Leq(dB) values.

- **decibel**: true --> adds live intensity (dB) plot with Leq average
- **voltage**: true --> shows live voltage counts
- **scaling**: true --> compute velocity using the *scaling_sensitivity* parameter. If disabled the plot shows voltage counts from the AD converter.

## alert_leq_IIR:
This module uses an IIR filter to compute the STA and LTA Leq, hence it doesn't require storing all the samples in the buffer. This allows to have longer LTA intervals while running without issue on light hardware (e.g. Raspberry Pi). 
IIR first order filter:

    y[n+1] = a * y[n] + (1-a) * x[n+1], where a ~ 10 ^ ( filter_loss[dB] / (20 * T * fs) )  ("remembering" factor)

- **a_sta**: "remembering" factor for the IIR filter for the STA calculation
- **a_lta**: "remembering" factor for the IIR filter for the LTA calculation
- **static_lta**: true --> use a static value for the LTA instead of an Leq calculation (preferred method, as varying LTA would contains also high noise events in the calculation)
- **lta**: Value for LTA if *static_lta* is set to true. Default 10dB (computed with 1 $\mu m/s$ (1e-6) dB reference).
- **scaling**: true --> compute velocity using the *scaling_sensitivity* parameter. If disabled the calculations are performed using voltage counts from the AD converter.


