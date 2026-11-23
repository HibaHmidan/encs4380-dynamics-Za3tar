# encs4380-dynamics-Za3tar
# ENCS4380 Homework 1: Dynamic Characteristics Interactive Toolkit

Birzeit University, ENCS4380 Interfacing Techniques (Instructor: Dr. Wasel Ghanem)

**Live site:** https://hibahmidan.github.io/encs4380-dynamics-Za3tar/

## Team members

| Name |
|------|
| Othman Katout |
| Hiba Hmidan |
| Hala Suboh |

## Who built which module

| Module | Owner | Status |
|--------|-------|--------|
| 1. First-order time response | Hiba | Done |
| 2. First-order frequency response | Hala | Done |
| 3. Second-order response | Othman | Done |
| 4. Guess the sensor | Hala | Done |

## Module 1: First-order time response (`index.html`)

A thermometer is a first-order sensor: it reads the past, smoothed. This page shows how the time constant τ and the gain K control how fast it responds.

**Model:** τ·dy/dt + y = K·x(t), with transfer function G(s) = K / (τs + 1)

### What you can do
- Choose the input: **step** or **ramp**.
- Move the sliders for **gain K** and **time constant τ**. All graphs redraw instantly.
- Answer the **"Predict, then check"** question before you move the sliders. It changes with the input type.

### What the page shows
- **Step response:** the output y(t) = K(1 − e^(−t/τ)), with markers at **63.2% at t = τ** and **95% at t = 3τ**.
- **Ramp response:** the output y(t) = K(t − τ + τe^(−t/τ)), with the **time lag (= τ)** and the **steady-state error** drawn on the graph.
- **Error fraction on a log axis:** the remaining error e^(−t/τ) is a straight line. Its slope is **−1/τ** for ln(error), and the page measures it from the curve.
- **Validation check 1:** y(τ) = 0.632·K and y(3τ) = 0.95·K, shown with expected value, calculated value and PASS/FAIL.

### Simplifications (chosen on purpose)
- Step height A = 1 and ramp slope A = 1.
- The sensor starts at y = 0.
- The ramp's steady-state error is τ in input units (x − y/K), and appears as K·τ on the graph because the graph shows the output y.
- The page measures the slope of ln(error) in natural log. The graph's axis is log base 10, so its visible slope is that value divided by 2.303.

## How to run it
Nothing to install. Open the live link above, or open `index.html` in any browser. It needs an internet connection, because the graphs use the Plotly library.
## Screenshots
### Module 2: First-order frequency response
<img width="767" height="438" alt="image" src="https://github.com/user-attachments/assets/1f0a29e8-409d-4ce8-a851-e58d00e73db8" />

### Module 4: Guess the sensor challenge

**Screenshot 1:**
<img width="1482" height="882" alt="image" src="https://github.com/user-attachments/assets/b990dd37-02e3-49f6-990c-8c1396f3751a" />

**Screenshot 2:**
<img width="1489" height="554" alt="image" src="https://github.com/user-attachments/assets/0d820c5a-0327-4f5b-af58-538d5b10e09b" />

### Module 3: Second-order response

**Screenshot 1:**
<img width="1917" height="908" alt="Screenshot 2026-11-12 192143" src="https://github.com/user-attachments/assets/cec0d479-aa35-49e1-ba26-22e11d572e7f" />

**Screenshot 2:**
<img width="1917" height="1020" alt="Screenshot 2026-11-12 192132" src="https://github.com/user-attachments/assets/3299c706-73d6-4035-bff2-8d659fb1f988" />



# Homework 2: PID Control Toolkit

| Module | Owner | ID | Status |
|--------|-------|-------|--------|
| P1. PID playground (+ validation checks) | Hiba Hmidan | 1230454 | Done |
| P2. A slow sensor in the loop | Hiba Hmidan | 1230454 | Done |
| [P3. Digital PID](P3.html) | Hala Suboh | 1230286 | Published (reference model) |
| P4. Tuning challenge | Othman Katout | 1230746 | Done |
| [My System (Micromouse drive motor)](my-system.html) | Hala Suboh | 1230286 | Published – motor measurements pending |

**Simulation:** each page runs its own solver. Every 1 ms step, the PID computes u = Kp·e + Ki·∫e dt + Kd·de/dt, then the plant moves forward with RK4. All metrics are read off the simulated curve.

## P1: PID playground (`p1.html`)
- Plant: first order K/(τs + 1) or second order Kωn²/(s² + 2ζωns + ωn²); the user sets Kp, Ki, Kd, the setpoint and the u limit.
- Shows the block diagram, output against setpoint, u with its limit, and live rise time (10–90%), overshoot, settling time (±2%) and steady-state error.
- Validation checks (K = 1, τ = 1 s): Kp = 9 gives τ = 0.1 s and 10% error; Kp = Ki = 1 gives ωn = 1 rad/s and ζ = 1; any PI gives zero steady-state error.
- No derivative kick: on the first step the previous error equals the current error.

## P2: A slow sensor in the loop (`p2.html`)
- A first-order sensor τs·dym/dt + ym = y sits in the feedback path, and the controller uses e = r − ym.
- Shows the true output y and the sensor reading ym on one plot, and how overshoot grows with τs until the loop oscillates.
- Plant fixed at K = 1, τ = 1 s; u limited to ±10.

## Screenshots (Homework 2)
P1:
<img width="393" height="470" alt="image" src="https://github.com/user-attachments/assets/c14f18af-948e-415d-80ea-ecfc89c6ad99" />

P2:
<img width="398" height="461" alt="image" src="https://github.com/user-attachments/assets/5e7c77b0-aeff-471a-a6e9-573f9cdd8ee3" />


## P4: Tuning challenge (`P4.html`)
- Plant: hidden first-order K/(τs + 1) or second-order Kωn²/(s² + 2ζωns + ωn²) system with randomized parameters and a "New random plant" button; the user tunes Kp, Ki, and Kd.
- Shows the output y against setpoint r = 1, control signal u with actuator limits (±20), and a live pass/fail specification table.
- Specifications: overshoot ≤ 10%, settling time (±2%) ≤ 2 s, steady-state error ≤ 1%, and |u| ≤ 20; reveals the hidden plant parameters once all specs pass.
- Solved with RK4 integration, clamping anti-windup, and no derivative kick.

## Screenshots (Homework 2)
## P4:-
<img width="1917" height="967" alt="Screenshot 2026-11-23 100535" src="https://github.com/user-attachments/assets/e3766717-91d9-48e7-ace2-20d0474e2611" />
<img width="1917" height="902" alt="Screenshot 2026-11-23 100549" src="https://github.com/user-attachments/assets/0cf6751e-1287-4246-a4d2-167eaf9220f0" />
<img width="1917" height="912" alt="Screenshot 2026-11-23 100558" src="https://github.com/user-attachments/assets/94830e6d-b28a-4b53-a53f-033a8504cf7a" />


## Tools used
- HTML and JavaScript, with [Plotly.js](https://plotly.com/javascript/) for the graphs.
- GitHub Pages for hosting.
- AI coding assistant (Claude): help write code based on the lecture formulas and the homework requirements, and to suggest fixes such as a time axis that scales with τ, drawing the ramp lag and steady-state error on the graph, and checking the validation numbers.

