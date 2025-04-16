---
layout: post
title: Hardware Components
date: 2023-06-10 19:03 -0500
author: Tresten Pool
categories: [Hardware]
tags: [Hardware, Assembly, Machine] 
image:
  path: /2023-06-10-hardware-components/profile.jpg
---

<!------------------------------------------------------->
<!------------ C COMPILATION & EXECUTION ---------------->
<!------------------------------------------------------->
## Index of Topics
---
> [Basics]()
>> + [How electricity works](#1.1)
>> + [Voltage](#1.2)
>> + [Current](#1.3)
>> + [Current](#1.4)
>> + [Types of Electricity](#1.5)

> [Usages]()
>> + [How home electricity works](#2.1)



<!------------------------------------------------------->
<!------------ HOW ELECTRICITY WORKS -------------------->
<!------------------------------------------------------->
<br><br><br>
### How electricity works <a id='1.1'></a>
---
- Electrons are **negatively charged**, meaning they flow from **negative to positive**

#### Electrons are the building blocks of understanding how electricity works
- **Conductors**
  - have very few electrons in the valance shell allowing them to move freely 
  - example
    - copper
    - silver
<br>
- **Insulators**
  - have many electrons in the valence shell not allowing the free electron to move freely
  - Example:
    - glass
    - rubber

#### Current (not appied/ applied) to copper wire
- With no current supplied to a copper wire, electrons are free and move randomly
  - ![no current](/2023-06-10-hardware-components/no_current.png)

- When current is applied to the copper wire via a battery, the free electrons will move in the a **circuit** from **negative to positive**
  - ![with current](/2023-06-10-hardware-components/current_applied.png)

#### (Closed / Open) Circuit
- Closed Circuit
  - ![closed circuit](/2023-06-10-hardware-components/closed_circuit.png)
- Open Circuit
  - ![open circuit](/2023-06-10-hardware-components/open_circuit.png)



<!------------------------------------------------------->
<!--------------------- VOLTAGE ------------------------->
<!------------------------------------------------------->
<br><br><br>
### Voltage (V) <a id='1.2'></a>
---


Water Analogy
  - ![voltage](/2023-06-10-hardware-components/voltage_1.png){: height="100"}
  - Like pressure in a water pipe. The more voltage means more pressure.
    - More pressure water can flow == More pressure electrons can flow
    - Voltage can exist *without current*
      - Just like how we can measure pressure in a water tank without it flowing
      - This is just measuring the pressure difference from the outside of the tank compared to inside the tank
      - We can measure the voltage with a multimeter with a **closed** and **open circuit**

What is a Volt
  - One Volt, is the force required to drive `one coulomb` through a resistor of `one ohm` in `one second`
  - Remember `1 coulomb` = 6.242 * 10 ^ 18
  - ![voltage](/2023-06-10-hardware-components/voltage_2.png){: height="100"}
  - `Volt = Joules / Coulomb`
    - Joule = Work
    - Coulomb = Group of flowing electrons

Voltage and Volts are different
  - **Voltage** is the pressure
  - **Volts** is the units we measure the pressure in

Potential Difference
  - You will hear this term used a lot for voltage
  - All this is saying is that **"how much work can potentially be done by a circuit"**

Voltage in Series
  - ![voltage](/2023-06-10-hardware-components/voltage_3.png){: height="100"}
    - if we cascade two batteries together in series, then the circuit will thus have more voltage, meaning a brighter light bulb

Voltage in Parallel
  - ![voltage](/2023-06-10-hardware-components/voltage_4.png){: height="100"}
    - If the two batteries are together in a parallel circuit, then the voltage stays the same because the electrons are split up, dividing the work into 2
    - In this example. The lamp is dimmer but powered for longer than if it was in series

Two lamps, One battery
  - ![voltage](/2023-06-10-hardware-components/voltage_5.png){: height="100"}
    - The image shows how the one battery powers both lamps across each at 0.75 splitting the voltage into two between the the two lamps

<!------------------------------------------------------->
<!--------------------- CURRENT ------------------------->
<!------------------------------------------------------->
<br><br><br>
### Current <a id='1.3'></a>
---
What is current
  - Current is the flow of electrons measured in **Amperes (Amps)** past a **single point** in a circuit within a set amount of time
  - Amps is also denoted by an `A`
  - `1 Amp = 1 Coulomb`
  - `1 Coulomb = 6,242,000,000,000,000,000 electrons per second`
  - In order test the current we need an **Ammeter** in series in the circuit to capture the current


<!------------------------------------------------------->
<!------------------ RESISTANCE ------------------------->
<!------------------------------------------------------->
<br><br><br>
### Resistance <a id='1.4'></a>
---
What is Resistance
  - Resistance is a *restriction* to the flow of electrons
  - Resistance is measured in Ohms

<br>
This example shows how size, material and temperature have resistance in a wire
  - ![resistance](/2023-06-10-hardware-components/resistance_1.png){: height="100"}

<br>
Resistors protect components by restricting the flow of current
  - ![resistance](/2023-06-10-hardware-components/resistance_2.png){: height="100"}


<!------------------------------------------------------->
<!------------ TYPES OF ELECTRICITY --------------------->
<!------------------------------------------------------->
<br><br><br>
### Types of Electricity <a id='1.5'></a>
---
![types](/2023-06-10-hardware-components/types_electricity.png){: height="100"}
<br>

1. Alternating Current (AC)
  - current moves back and forth with the changing magnetic field
  - used in wall sockets at home

2. Direct Current (DC)
  - Current travels only in one direction 
  - used in circuits that contain batteries


<!------------------------------------------------------->
<!--------------- HOME ELECTRICITY ---------------------->
<!------------------------------------------------------->
<br><br><br>
### Electricity at Homes <a id='2.1'></a>
---

- ![types](/2023-06-10-hardware-components/types_electricity.png){: height="100"}
  - Electricity is produced at the power plant
    - Voltage is increased and connected to the grid and transferred over long distances 





<!------------------------------------------------------->
<!--------------------- REFERENCES ---------------------->
<!------------------------------------------------------->
<br><br><br>
## REFERENCES
---
- {% include embed/youtube.html id='mc979OhitAg' %}