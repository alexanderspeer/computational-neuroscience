# Computational Neuroscience Portfolio

Alexander Speer (aes2376) — Columbia University

Coursework and projects from two graduate-level computational neuroscience courses at Columbia:
- **BMEB W4020** — Circuits in the Brain (Fall 2025), Prof. Aurel A. Lazar
- **ECBM E4070/6070** — Computing with Brain Circuits of Model Organisms (Spring 2026), Prof. Aurel A. Lazar

All work is implemented in Python (NumPy, SciPy, Matplotlib) in Jupyter notebooks.
Most assignments were completed in collaboration with Andre Perez (avp2141) or Ciro Randazzo (cr3510).

---

## Technical Skills Demonstrated

### Biophysical Neuron Modeling

- **Morris-Lecar model**: numerical ODE integration (Euler method), spike detection, phase-plane analysis, limit cycle characterization, bifurcation across input current amplitudes.
- **Rinzel model (reduced Hodgkin-Huxley)**: limit cycle extraction, iPRC computation, stable orbit simulation.
- **Hodgkin-Huxley neuron**: full conductance-based simulation, F-I characterization, threshold analysis.
- **Connor-Stevens neuron**: A-current dynamics, F-I curve analysis, comparison with HH threshold behavior.
- **Non-spiking Hodgkin-Huxley neuron (HHNS)**: graded voltage output as part of photoreceptor cascade.
- **ECG model (BVAM)**: simulation of healthy and pathological (sinus tachycardia) cardiac rhythms using a coupled nonlinear ODE model of SA and AV nodes.

### Phase Response and Reduction Theory

- **Winfree's method** for numerically approximating the Phase Response Curve (PRC) of arbitrary limit-cycle oscillators, applied to: Rinzel neuron, HH neuron, ECG BVAM model (SA node and AV node).
- **iPRC computation** (infinitesimal PRC) and use in model reduction.
- **Project-Integrate-and-Fire (PIF) neuron**: construction of a linear equivalent reduced model calibrated from the iPRC and limit cycle period; spike timing comparison against the full Rinzel neuron.
- **Synaptic perturbation analysis**: modeling synaptic current as a perturbation and computing its effect on spike times via the PRC.

### Time Encoding and Decoding (TEM/TDM)

- **Asynchronous Sigma-Delta Modulator (ASDM)**: forward-Euler integrator implementation, threshold-based spike emission.
  - δ-sensitive decoding: reconstruction via sinc basis, G matrix (Gram matrix of basis integrals over ISIs), pseudoinverse solve.
  - δ-insensitive decoding (Compensation Principle): augmented system [G | h][c; K] to eliminate threshold as unknown.
  - SNR analysis: whole-signal and time-resolved SNR, comparison across decoders.
- **Ideal Integrate-and-Fire (IAF) neuron** TEM/TDM: encoding via biased trapezoidal integration, decoding via the same G/q framework; effect of bias on spike density and reconstruction quality.
- **ON-OFF signal separation**: half-wave rectification (ReLU) into ON and OFF channels, independent IAF encoding/decoding of each channel, combined reconstruction u_hat_on - u_hat_off, SNR comparison across bias values and channel types.
- **Trigonometric polynomial stimulus space**: random trig-poly signal generation, FFT-based coefficient extraction, Fourier-domain analysis of stimuli and recovered filters.

### Dendritic Filter Identification

- **[Filter]-[IAF] cascade identification**: given spike times from an IAF driven by a filtered stimulus, recover the unknown dendritic filter h(t) projected onto the trigonometric polynomial space.
  - Construction of the Φ matrix (inner products of basis functions with shifted inputs over spike intervals).
  - Pseudoinverse or regularized least-squares (Tikhonov) solve for filter Fourier coefficients.
  - MSE analysis vs. stimulus bandwidth (25, 50, 100 Hz).
- **Multiple I/O pairs**: combining spike data from several stimuli to improve filter estimation (Theorem 11.3).
- **Two-filter dendritic circuit**: identification of h1(t) and h2(t) jointly from a two-channel input driving a shared IAF neuron; full derivation of the augmented linear system and block Φ matrix.
- **[Filter]-[ON-OFF-IAF-with-feedback] circuit** (HW6): spatiotemporal filter identification from an ON-OFF AER neuron with self- and cross-feedback temporal filters. T-transform derivation in inner product form; construction of Φ matrix in 3D trig-polynomial space (spatial x, y and temporal t basis).
- **Noisy thresholds**: IAF identification under Gaussian random thresholds; Tikhonov regularization for stability; MSE vs. bandwidth analysis across 10–80 Hz.

### Sensory Transduction Models

- **Drosophila photoreceptor (reduced OTP model)**: 3-state ODE system (x1, x2, x3) driven by light intensity λ, modeling phototransduction via TRP channels with divisive normalization conductance; coupled to a non-spiking HH membrane.
  - Steady-state sigmoidal V vs. log(I) curve.
  - Divisive normalization parameter sweeps (a1, a2, c1, c2).
- **Feedforward/feedback divisive normalization circuit**: Volterra series representation of T1 and T2 operators (zero-order, first-order kernel H1, second-order kernel H2); analytical steady-state derivation; feedback operator T3 analysis.
- **Olfactory Transduction Pathway (OTP) / Active Receptor Model**: simulation of the olfactory receptor neuron cascade; step, ramp, and parabola concentration stimuli; ligand-receptor affinity effects.
- **OTP/BSG cascade** (OTP + Connor-Stevens or HH as Biophysical Spike Generator): temporal I/O and steady-state F-I (firing rate vs. concentration) characterization; comparison of CS and HH behavior in cascade.

### Insect Visual System Modeling (ECBM Project 1)

Implementation of a **Directionally Selective Small Target Motion Detector (DSTMD)** neural network (Wang et al., IEEE Trans. Cybernetics 2020) modeling the insect visual system:
- **Retina layer**: Gaussian blur (ommatidium model).
- **Lamina layer**: temporal band-pass filtering via Gamma kernel difference (LMC model); lateral inhibition.
- **Medulla layer**: ON/OFF signal separation; temporal delay modeling of Mi1 and Tm1/Tm2/Tm3 neurons via Gamma kernels.
- **Lobula layer**: DSTMD correlation mechanism (two-position signal correlation for direction selectivity); second-order lateral inhibition for size selectivity; direction-angle lateral inhibition.
- **Population vector algorithm** for motion direction estimation.
- Evaluation on cluttered background image sequences.

### Full Biophysical Cascade: Project 2 (BMEB W4020)

End-to-end encoding and decoding of a black-box biophysical neuron consisting of:
- Two-channel **dendritic tree** (linear spatiotemporal filters).
- **ON-OFF AER axon hillock** (Address Event Representation neuron).

Tasks: signal injection in Dendrite or Axon mode, spike train analysis, and system identification of the unknown dendritic filter from spike data alone.

---

## Repository Structure

```
comp-neuro-repo/
├── README.md
├── images/                          # Figures exported from notebooks
├── BMEBW4020 Comp Neuro Circuits in the Brain/
│   ├── hw1/    Morris-Lecar model, phase-plane analysis
│   ├── hw2/    PRC (Rinzel), PIF neuron, synaptic perturbation
│   ├── hw3/    ASDM TEM/TDM, ON-OFF IAF, SNR analysis
│   ├── hw4/    Filter-Rinzel-BSG cascade, TEM/TDM derivation
│   ├── hw5/    Filter identification, two-filter circuit, trig-poly space
│   ├── hw6/    Spatiotemporal filter ID, ON-OFF feedback, noisy thresholds
│   ├── project1/  ECG BVAM model, cardiac PRC (SA and AV nodes)
│   └── project2/  Biophysical neuron (dendritic tree + ON-OFF AER) identification
└── ECBM4070E Computing with Brain Circuits of Model Organisms/
    ├── hw2/    Drosophila photoreceptor, divisive normalization circuit
    ├── hw3/    ASDM/IAF TEM/TDM, ON-OFF nonlinear circuit
    ├── hw4/    OTP/BSG cascade, Connor-Stevens vs HH I/O characterization
    └── project1/  DSTMD insect visual system (Wang et al. 2020)
```

---

## Key Methods by Topic

| Topic | Methods / Models |
|---|---|
| Neuron modeling | Morris-Lecar, Rinzel, HH, Connor-Stevens, HHNS, IAF, ASDM, AER |
| Model reduction | PRC (Winfree), iPRC, PIF equivalence, limit cycle extraction |
| Encoding theory | ASDM, IAF, TEM t-transform, G/Φ matrix, sinc/trig-poly basis |
| Decoding theory | Pseudoinverse, Tikhonov regularization, δ-sensitive/insensitive |
| Filter identification | [Filter]-[IAF], two-filter circuit, spatiotemporal filter, noisy thresholds |
| Sensory systems | Photoreceptor ODE, TRP/divisive normalization, OTP, ON/OFF pathways |
| Visual neuroscience | DSTMD, ESTMD, LMC, lateral inhibition, direction selectivity, population vector |
| Signal analysis | SNR (whole-signal and time-resolved), MSE vs. bandwidth, F-I curves |
| Math tools | Volterra series, trig-polynomial spaces, Fourier analysis, inner products, ODE integration |

---

## Selected Figures

Output figures from key experiments are collected in `images/`. These include phase-plane plots, limit cycles, filter reconstructions, SNR traces, F-I curves, and DSTMD detection results.

---

## Reference

Wang, H., Peng, J., and Yue, S. (2020). A Directionally Selective Small Target Motion Detecting Visual Neural Network in Cluttered Backgrounds. *IEEE Transactions on Cybernetics*, 50(4), 1541–1555.
