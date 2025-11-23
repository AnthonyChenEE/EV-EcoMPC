# EV-EcoMPC

An open-source project for **energy-efficient electric vehicle (EV) control** using **Model Predictive Control (MPC)**.  
The goal is to compute an acceleration profile that minimizes traction energy while respecting speed and acceleration limits.

This repo includes:
- A basic longitudinal EV model  
- Rolling resistance + aerodynamic drag  
- A convex MPC controller (CVXPY)  
- Example scripts for flat routes  
- Clean, easy-to-extend project structure  

---

## Installation

```bash
git clone https://github.com/AnthonyChenEE/EV-EcoMPC.git
cd EV-EcoMPC
pip install -r requirements.txt
````

---

## Quick Start

Run the simple MPC example:

```bash
python examples/simple_flat_route.py
```

This will plot:

* Speed vs time
* Acceleration vs time
* Position vs time

---

## Project Structure

```
EV-EcoMPC/
├─ src/
│  ├─ models/            # EV model
│  ├─ mpc/               # MPC solver
│  └─ utils/             # route + plotting
├─ examples/             # ready-to-run demos
├─ data/                 # sample route data
└─ tests/                # basic tests
```

---

## Basic Idea

States:

* ( v ): speed
* ( s ): position

Control:

* ( a ): acceleration

Dynamics:

* ( v_{k+1} = v_k + T_s a_k )
* ( s_{k+1} = s_k + T_s v_k )

Energy cost:

* Rolling resistance
* Aerodynamic drag
* Positive traction power

The MPC minimizes total traction energy over a finite horizon.

---

## Example Code (minimal)

```python
from src.mpc.eco_mpc_cvxpy import solve_eco_mpc

v, s, a = solve_eco_mpc(
    N=30,
    Ts=0.5,
    v0=0.0,
    s0=0.0
)
```

---

## License

MIT License — free to use and modify.

---

## Notes

This project is for **research and education only**.
Not affiliated with any automaker or company.
