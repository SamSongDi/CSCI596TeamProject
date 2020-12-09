# Study of parallel computing techniques for simulation optical beam propagation in atmospheric turbulence
## Team members

Hao Song (songhao@usc.edu)

Kaiheng Zou (kaihengz@usc.edu )

HUibin Zhou (huibinzh@usc.edu)

Xinzhou Su (xinzhous@usc.edu )

## Goal (What's the "big" problem? Why important?)

![Concept](Figures/Concept.png)

## Scientific objectives

### Step 1:

Apply OpenMP techniques in simulating the multiple realizations of the turbulence effect on the optical beam with different wavelengths and orthogonal spatial modes.

### Step 2: 

Use CUDA techniques in simulating the Fourier transform-based beam propagation process.

### Step 3: 

Evaluate the efficiency of the simulation when tuning different parameters.

### Step 4: 

Adjust the code to maximize the efficiency under different conditions.

## Previous work

## Potential techniques to use

![Model](Figures/model.png)
Simulation model and parallel programing techniques used in simulating turbulence effects on optical beams.

To study the influence of atmospheric turbulence on optical beams, we first build a model to emulate the turbulence. According to Kolmogorov turbulence theory, the refractive index fluctuation caused by atmospheric turbulence can be described by a structure function Dn, which is determined by

Dn(Δr)=6.88(Δr/r0)5/3

where Δr is the distance between two points in space, and r0 is the Fried parameter, or the coherence length. Assuming the value of Cn2 keeps unchanged over propagation path, r0 can be calculated from the atmospheric structure constant Cn2 by the formula

r0=(0.423k2Cn2L)-3/5

where k=2/f is the wave number and L is the propagation length.

Based on the above equations, the turbulence can be simulated by using phase plates, which can be described as N-by-N matrices of random phase numbers with statistics that match Kolmogorov turbulence theory. The simulation model is shown in the figure. The input optical signal with single wavelength and single spatial mode is applied by the phase changes on each pixel defined by the phase plates. The phase plates are generated according to the abovementioned Kolmogorov theory to emulate the atmospheric turbulence. After certain amount of phase plates, an output beam is generated as the beam with the turbulence effect. The beam propagation is modeled with the Fourier transform-based method by

Eout=F-1{F{Ein}·H(λ,z)}

where Ein and Eout are the electrical fields of the beam before and after propagation. F-1 and F denote the inverse Fourier and Fourier transforms. H(λ,z) is the spectral transfer function of the propagation as a function of the wavelength λ and the propagation distance z.

In such a simulation model, there are several places that different parallel programming techniques can be used to accelerate the simulation, as shown in the figure. In a typical free-space optical communication system, multiple wavelengths and multiple spatial modes are used to increase the data capacity. These wavelengths and spatial modes are orthogonal, meaning that they have little influence over each other. Therefore, we can use OpenMP to simulate the turbulence effect on these optical beams with different wavelengths and spatial modes. To show a better modelling of a dynamic turbulence effect, we need to simulate multiple realizations of the emulating phase plates. We can also use OpenMP to simulate the different realizations. The Fourier transform in the propagation process is implemented by the fast Fourier transform (FFT) algorithm, which is also shown in the model figure. We can use the cuFFT of the GPU accelerated CUDA for the FFT simulation.

## Expected results

### Preliminary results

![FixedScaling](Figures/CPU_turbulenceRealization_fixed.png)

![IsoScaling](Figures/CPU_turbulenceRealization_isogranular.png)

### What's the our next step?

