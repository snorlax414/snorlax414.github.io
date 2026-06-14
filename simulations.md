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

<iframe width='800' height='400' src='https://www.wolframcloud.com/obj/3f9e64ec-99af-4301-b34a-f3f38f95f3f1' frameborder='0'></iframe>

> 💡 **Tip:** If the interactive panels fail to respond, refresh the page to clear the cloud container state.
