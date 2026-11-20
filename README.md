# Magnetic Field Simulator

Lukas Schreyögg · Physics B.Sc., TU Munich

I wanted to actually *see* the fields from magnetostatics instead of only computing them on paper, so I built this simulator. You pick a configuration (a straight wire, two parallel wires, a single loop, a Helmholtz pair, an anti-Helmholtz pair or a solenoid), move the sliders for current, number of turns, radius and spacing, and the field map and field lines update right away. These are most of the configuration you will need for Electrodynamics in your physics course

**Try it:** https://lukasschreyoegg.github.io/magnetic-field-simulator/

## How it works

Everything comes from the Biot–Savart law. For straight wires I just add up μ₀I/(2πr). For circular loops the integral around the ring can be written in closed form with the complete elliptic integrals K and E, which I evaluate with the arithmetic–geometric mean. Every coil is then a sum of loops.

The field lines are traced with a 4th-order Runge–Kutta step along B/|B|. For the coils I start them at points of equal magnetic flux, so where the lines are dense the field is actually strong.

## Does it give the right numbers?

I wanted to be sure the general solution is correct, so the app checks itself against the formulas we know exactly:

- On the axis of a loop: B = μ₀NIR² / (2(R² + z²)^{3/2}). The two agree to about 10⁻¹³ %.
- Helmholtz pair (d = R): the centre field is (4/5)^{3/2} μ₀NI/R, which gives 0.899 mT for R = 10 cm, N = 100, I = 1 A. At z = R/4 the field has dropped by only 0.42 %, which is the 4th-order term you expect.
- Finite solenoid: B(0) divided by μ₀NI/L comes out as L/√(L² + 4R²), as it should.

## Next step

I'm planning to build a small Helmholtz coil and measure its field with a Hall sensor. This simulator is the reference curve I will compare the measurement to.

## Limitations

Thin wires, all turns of a coil sitting at one position, static currents, vacuum.

## Running it

Open `index.html` in any browser. It's a single file with plain JavaScript and no libraries, so it also works offline.

## How it was made

I built this together with Claude (Anthropic) as a coding assistant. The idea, the choice of configurations and physics, and the checks against the analytic results are mine. Most of the JavaScript was written by Claude.
