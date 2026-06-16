---
layout: default
title: Computational Simulation
---

<script type="text/javascript" async
  src="https://cdnjs.cloudflare.com/ajax/libs/mathjax/2.7.7/MathJax.js?config=TeX-MML-AM_CHTML">
</script>

# About

The following simulation is that of a series LCR circuit's behaviour, connected to a 220V AC supply.
The parameters evaluated are its impedance and variation of current output over a frequency range.

## Brief Theory

The components of an LCR circuit include a resistor, a capacitor and an inductor. The impedance of the circuit is the effective 'opposition' to current flow. It is measured in $$\Omega$$ (ohms). 

The formula of impedance ($$Z$$) is given by:

<p>$$Z = \sqrt{R^2 + (X_L - X_C)^2}$$</p>

Where:
* $$R$$ is the resistance
* $$X_L = \omega L$$ is the inductive reactance
* $$X_C = \frac{1}{\omega C}$$ is the capacitive reactance

It is seen that impedance is dependent on frequency of the source. The maximum current ($$I_0$$) in an AC circuit is measured as:

<p>$$I_0 = \frac{V_0}{Z}$$</p>

From both formulae it is apparent that as the frequency increases, impedance value drops to a pit and then slowly increases again, and current value increases, peaks to a point and falls off again. The value of frequency at which current peaks is called **resonant frequency**, where the opposition to current is least. In that case, $$Z = R$$, which means $$X_L = X_C$$, i.e.,

<p>$$\omega = \frac{1}{\sqrt{LC}}$$</p>

## How the Simulation Works

1. **Dynamic Control (*Manipulate*):** The sliders on the interface bind the physical parameters—Resistance ($$R$$), Inductance ($$L$$), Capacitance ($$C$$), and Source Voltage ($$V_0$$)—to dynamic variables.
2. **Frequency Sweeping (*Table* / *Plot*):** The code computes the impedance $$Z$$ and current $$I_0$$ across a continuous frequency range $$\omega$$. It then feeds these values into a real-time plotting function.
3. **Resonance Calculation:** The simulation continuously calculates the exact mathematical root where $$X_L = X_C$$ to dynamically highlight the resonant peak on the graph as the sliders are moved.
4. **Cloud Deployment (*CloudDeploy*):** The entire evaluation loop is deployed to the Wolfram Cloud, which handles the computation server-side and renders the interface inside the website's `<iframe>`.
5. On altering the resistance slider, the peaks show increase or decrease in sharpness. On altering Capacitance or Inductance slider, the graphs shows lateral movement.
6. On altering source voltage slider, peak current value increases or decreases.

Below is the live, interactive simulation deployed via the Wolfram Cloud.

<iframe width='800' height='400' src='https://www.wolframcloud.com/obj/3e32e9fe-f323-4b61-a5f0-adbc95267752' frameborder='0'></iframe>

<br>
<details>
  <summary style="cursor: pointer; font-weight: bold; color: #0066cc; font-size: 1.1em; user-select: none;">
    ▶ Click to View Wolfram Language Source Code
  </summary>
  
  <br>

```wolfram
Manipulate[
  Module[{w0, maxCurrent, impedanceCurve, currentCurve},
    w0 = 1/Sqrt[L*C];
    maxCurrent = V0/R;
    
    (* CloudDeploy[
 Manipulate[
  Module[{w0, maxCurrent, impedanceCurve, currentCurve}, 
   w0 = 1/Sqrt[L*C];
   maxCurrent = V0/R;
   impedanceCurve = 
    Plot[Sqrt[R^2 + (w*L - 1/(w*C))^2], {w, 10, 1000}, 
     PlotStyle -> {Blue, Thick}, 
     AxesLabel -> {"Frequency (\[Omega])", "Impedance (Z)"}, 
     PlotLabel -> Style["Impedance vs Frequency Curve", Bold, 12], 
     PlotRange -> {0, 300}, GridLines -> {{w0}, {R}}, 
     GridLinesStyle -> Directive[Gray, Dashed], 
     Epilog -> {Red, PointSize[0.02], Point[{w0, R}], 
       Text[Style["Minimum Z = R", Darker[Gray], 10], {w0 + 100, 
         R + 15}]}, ImageSize -> 350];
   currentCurve = 
    Plot[V0/Sqrt[R^2 + (w*L - 1/(w*C))^2], {w, 10, 1000}, 
     PlotStyle -> {Darker[Green], Thick}, 
     AxesLabel -> {"Frequency (\[Omega])", 
       "Peak Current (\!\(\*SubscriptBox[\(I\), \(0\)]\))"}, 
     PlotLabel -> Style["Current Resonance Curve", Bold, 12], 
     PlotRange -> {0, maxCurrent + 0.5}, 
     GridLines -> {{w0}, {maxCurrent}}, 
     GridLinesStyle -> Directive[Gray, Dashed], 
     Epilog -> {Red, PointSize[0.02], Point[{w0, maxCurrent}], 
       Text[Style["Max Current", Darker[Gray], 10], {w0 + 100, 
         maxCurrent - 0.2}]}, ImageSize -> 350];
   Column[{Text@
      Style[Row[{"Calculated Resonant Frequency (\!\(\*SubscriptBox\
[\(\[Omega]\), \(0\)]\)): ", NumberForm[w0, {5, 2}], " rad/s"}], 12, 
       Bold, Darker[Blue]], Spacer[10], 
     Row[{impedanceCurve, Spacer[15], currentCurve}]}, 
    Alignment -> Center]], {{R, 20, "Resistance (R in Ω)"}, 5, 100, 1,
    Appearance -> "Labeled"}, {{L, 0.2, "Inductance (L in H)"}, 0.05, 
   1.0, 0.01, 
   Appearance -> "Labeled"}, {{C, 0.00005, "Capacitance (C in F)"}, 
   0.00001, 0.0002, 0.00001, 
   Appearance -> "Labeled"}, {{V0, 220, 
    "Source Voltage (\!\(\*SubscriptBox[\(V\), \(0\)]\) in V)"}, 100, 
   440, 10, Appearance -> "Labeled"}, TrackedSymbols :> {R, L, C, V0}],
  Permissions -> "Public"] *)
    
  ]
]



> 💡 **Tip:** If the interactive panels fail to respond, refresh the page to clear the cloud container state.
