# Basic electronics

- [Basic electronics](#basic-electronics)
  - [Electricity principles](#electricity-principles)
    - [Electricity flow](#electricity-flow)
    - [What is Voltage?](#what-is-voltage)
    - [What is Current?](#what-is-current)
      - [Direct Current (DC) vs Alternating Current (AC)](#direct-current-dc-vs-alternating-current-ac)
    - [What is resistance?](#what-is-resistance)
    - [What is Power and Joule’s Law?](#what-is-power-and-joules-law)
    - [Kirchhoff's Laws](#kirchhoffs-laws)
      - [Kirchhoff's current law](#kirchhoffs-current-law)
      - [Kirchhoff's voltage law](#kirchhoffs-voltage-law)

## Electricity principles

### Electricity flow

The conventional direction of current, first defined by [Benjamin Franklin](https://en.wikipedia.org/wiki/Benjamin_Franklin), that became known as conventional current, is from positive to negative. The positively charged particle are free to move and the negatively charged particles are fixed, so positive moves towards negative.

Later [J. J. Thomson](https://en.wikipedia.org/wiki/J._J._Thomson) discovered the [electron](https://en.wikipedia.org/wiki/Electron) which is negatively charged, and consequently that the flow of electricity is from negative to positive.

> The conventional direction of current, also known as conventional current, is arbitrarily defined as the direction in which positive charges flow. In a conductive material, the moving charged particles that constitute the electric current are called charge carriers. In metals, which make up the wires and other conductors in most electrical circuits, the positively charged atomic nuclei of the atoms are held in a fixed position, and the negatively charged electrons are the charge carriers, free to move about in the metal. In other materials, notably the semiconductors, the charge carriers can be positive or negative, depending on the dopant used. Positive and negative charge carriers may even be present at the same time, as happens in an electrolyte in an electrochemical cell.
>
> A flow of positive charges gives the same electric current, and has the same effect in a circuit, as an equal flow of negative charges in the opposite direction. Since current can be the flow of either positive or negative charges, or both, a convention is needed for the direction of current that is independent of the type of charge carriers. Negatively charged carriers, such as the electrons (the charge carriers in metal wires and many other electronic circuit components), therefore flow in the opposite direction of conventional current flow in an electrical circuit.
>
> **Reference direction**
>
> A current in a wire or circuit element can flow in either of two directions. When defining a variable _I_ to represent the current, the direction representing positive current must be specified, usually by an arrow on the circuit schematic diagram. This is called the reference direction of the current _I_. When analyzing electrical circuits, the actual direction of current through a specific circuit element is usually unknown until the analysis is completed. Consequently, the reference directions of currents are often assigned arbitrarily. When the circuit is solved, a negative value for the current implies the actual direction of current through that circuit element is opposite that of the chosen reference direction.

[Wikipedia - Electric current](https://en.wikipedia.org/wiki/Electric_current#Conventions)

![Flow of electricity](https://upload.wikimedia.org/wikipedia/commons/2/2e/Current_notation.svg "The electrons, the charge carriers in an electrical circuit, flow in the opposite direction of the conventional electric current.")

### What is Voltage?

> Voltage, also known as **(electrical) potential difference, electric pressure**, or **electric tension** is the difference in electric potential between two points. In a static electric field, it corresponds to the work needed per unit of charge to move a positive test charge from the first point to the second point. In the International System of Units (SI), the derived unit for voltage is the volt (V).

[Wikipedia - Voltage](https://en.wikipedia.org/wiki/Voltage)

Voltage can be seen as the force needed to move a charged particle (electron) inside a wire. Volts is the unit used to describe the strength of this force. When applying Voltage to a circuit it causes the electrons to move along the wires and the flow of electrons in a wire is [Electric Current](https://en.wikipedia.org/wiki/Electric_current).

### What is Current?

> An **electric current** is a flow of charged particles, such as electrons or ions, moving through an electrical conductor or space. It is defined as the net rate of flow of electric charge through a surface.

[Wikipedia - Electric current](https://en.wikipedia.org/wiki/Electric_current)

Current is denoted by the letter _I_. We use the unit [Ampere](https://en.wikipedia.org/wiki/Ampere) (often shortened to amp) as a measure of electric current. Amperes represent a number of charged particles (often electrons) that go through a section of a conductor in 1 second.

We can calculate current, with the following equation. Where _I_ is the current in Amperes, _Q_ is the quantity of charge in Coulombs, and _t_ is the time in seconds.

$$
I=\frac{Q}{t}
$$

> The unit of charge, the [coulomb](https://en.wikipedia.org/wiki/Coulomb), "is the quantity of electricity carried in 1 second by a current of 1 ampere". Conversely, a current of one ampere is one coulomb of charge going past a given point per second:

$$
1A=1C/s
$$

What is Alternating Current?

#### Direct Current (DC) vs Alternating Current (AC)

> Direct current (DC) is one-directional flow of electric charge.

- [Wikipedia - Direct current](https://en.wikipedia.org/wiki/Direct_current)
- [Circuit Basics - What is direct current?](https://www.circuitbasics.com/what-is-current)

Direct Current as a constant voltage supply. So a 5V DC constantly supplies 5 volts of power.

> Alternating current (AC) is an electric current that periodically reverses direction and changes its magnitude continuously with time, in contrast to direct current (DC), which flows only in one direction.

- [Wikipedia - Alternating current](https://en.wikipedia.org/wiki/Alternating_current)
- [Circuit Basics - What is direct current?](https://www.circuitbasics.com/what-is-alternating-current)

As the name suggest Alternating current as a alternating voltage supply. A 220V AC alternates between 110V and -110V.

![Graph comparing different current types](https://upload.wikimedia.org/wikipedia/commons/thumb/3/38/Types_of_current.svg/2880px-Types_of_current.svg.png "Direct current (DC) (red line). The vertical axis shows current or voltage and the horizontal 't' axis measures time and shows the zero value.")

### What is resistance?

> The electrical resistance of an object is a measure of its opposition to the flow of electric current.
>
> ...
>
> The resistance of an object depends in large part on the material it is made of. Objects made of electrical insulators like rubber tend to have very high resistance and low conductance, while objects made of electrical conductors like metals tend to have very low resistance and high conductance. This relationship is quantified by resistivity or conductivity. The nature of a material is not the only factor in resistance and conductance, however; it also depends on the size and shape of an object because these properties are extensive rather than intensive. For example, a wire's resistance is higher if it is long and thin, and lower if it is short and thick. All objects resist electrical current, except for superconductors, which have a resistance of zero.

[Wikipedia - Electrical resistance and conductance](https://en.wikipedia.org/wiki/Electrical_resistance_and_conductance)

The unit that measures electrical resistance is the [ohm (Ω)](https://en.wikipedia.org/wiki/Ohm).

> Ohm's law states that the electric current through a conductor between two points is directly proportional to the voltage across the two points. Introducing the constant of proportionality, the resistance, one arrives at the three mathematical equations used to describe this relationship:
>
> $$
> V = I \times R <=> I = \frac{V}{R} <=> R = \frac{V}{I}
> $$

### What is Power and Joule’s Law?

> Power is the term used to describe the rate of doing work or work over time. This means that a 100W lightbulb is running much hotter than a 1W lightbulb, and we can sense the work being done by the heat generated. Power is directly linked to Ohm’s by Joule’s law, which says that the heat produced in resistance is proportional to the square of the current flowing through it over a given time.
>
> We can express this as $P = V \times I$ and because $V = I \times R$, we get $P = I \times I \times R$ or $P = I^{2} \times R$. In the same way $P=\frac{V^{2}}{R}$.
>
> Energy is defined as “the property that must be transferred to an object to perform work on, or to heat, the object. Energy is a conserved quantity; the law of energy conservation states that energy can be converted in form but not created or destroyed. The SI unit of energy is the joule, which is the energy transferred to an object by the work of moving it a distance of one meter against a force of one newton”. And 1W is 1 Joule spent in 1 second.

Energy can be expressed as follows:

$$
E = P \times t(seconds)
$$

[Circuit Basics - Ohm’s Law, Power and Energy](https://www.circuitbasics.com/ohms-law-power-and-energy/)

### Kirchhoff's Laws

[Wikipedia - Kirchhoff's circuit laws](https://en.wikipedia.org/wiki/Kirchhoff%27s_circuit_laws)

#### Kirchhoff's current law

> The current entering any junction is equal to the current leaving that junction. This law, also called Kirchhoff's first law, or Kirchhoff's junction rule, states that, for any node (junction) in an electrical circuit, the sum of currents flowing into that node is equal to the sum of currents flowing out of that node; or equivalently:
>
> _The algebraic sum of currents in a network of conductors meeting at a point is zero._
>
> Recalling that current is a signed (positive or negative) quantity reflecting direction towards or away from a node, this principle can be succinctly stated as:
>
> $$
> \sum^n_{\substack{i=1}}I_i=0
> $$
>
> where _n_ is the total number of branches with currents flowing towards or away from the node.
>
> ![Kirchhoff's current law schematics](https://upload.wikimedia.org/wikipedia/commons/thumb/4/46/KCL_-_Kirchhoff%27s_circuit_laws.svg/1024px-KCL_-_Kirchhoff%27s_circuit_laws.svg.png "Kirchhoff's current law schematics")

#### Kirchhoff's voltage law

> This law, also called Kirchhoff's second law, or Kirchhoff's loop rule, states the following:
>
> _The directed sum of the potential differences (voltages) around any closed loop is zero._
>
> Similarly to Kirchhoff's current law, the voltage law can be stated as:
>
> $$
> \sum^n_{\substack{i=1}}V_i=0
> $$
>
> Here, _n_ is the total number of voltages measured.
>
> ![Kirchhoff's voltage law schematics](https://upload.wikimedia.org/wikipedia/commons/thumb/4/40/Kirchhoff_voltage_law.svg/1024px-Kirchhoff_voltage_law.svg.png "Kirchhoff's voltage law schematics")
