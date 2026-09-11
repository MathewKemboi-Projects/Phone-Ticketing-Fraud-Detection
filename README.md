# Phone-Ticketing-Fraud-Detection
Extending a card-based transit fraud detection model to phone/account-based ticketing — including a genuinely new fraud check specific to account-based systems.



Overview

Physical transit cards can only be in one place at a time. Phone-based ticketing, tied to a login rather than a physical object, opens a new fraud path: account sharing across multiple devices. This project demonstrates two fraud checks side by side:

Impossible travel — the same account tapping in at two stations too far apart to have travelled between in the time elapsed (the same physics-based technique banks use for stolen-card detection).
Simultaneous multi-device use (new) — the same account tapping in on two different devices within seconds of each other. A physical card structurally can't do this without cloning; a shared login can, trivially.

Both checks are grounded in real Dublin transport station geography (Luas + DART coordinates) and evaluated honestly against known, injected ground truth — not just asserted.

Results (verified, not asserted)
Metric	Value
True fraud accounts (synthetic, injected)	14
Correctly flagged	13
False positives	1
Combined recall	93%
Combined precision	93%
Impossible travel recall	83% (5/6)
Simultaneous multi-device recall	100% (8/8)

Run python tests/run_tests.py (or the notebook's evaluation cell) to reproduce these numbers yourself.

Why this structure

Most fraud-detection demos apply one technique and stop. This project deliberately shows two checks — one reused unchanged from a prior card-based project, one genuinely new — to demonstrate the difference between porting a technique and extending it with domain-specific reasoning. Part 6 of the notebook explains, in plain terms, exactly why account-based ticketing needs a check that card-based ticketing structurally doesn't.

Visualisations
Interactive map (Plotly) — every flagged event plotted on real Dublin station geography, colour-coded by fraud type, with hover details showing account, stations, and reasoning.
Detection performance charts — recall/precision broken down by fraud type, computed dynamically from actual results (nothing hardcoded).
Data — an honesty note

All data is synthetic, generated in the notebook itself using real Dublin Luas/DART station coordinates and the haversine (great-circle distance) formula. This is a methodology demonstration, not real transit data. See the companion project below for a version of the "impossible travel" check validated against real, independently verifiable data (two real hurricanes correctly flagged in real bike-share demand data).

Related projects
transport-card-fraud-detection — the original card-based version this project extends
retail-demand-forecasting — the same "test on real data, report honest results" approach, validated against real historical data (including two correctly-flagged real hurricanes)
Tech

Python · pandas · NumPy · Plotly · Matplotlib · Haversine distance calculation (no external geo library required)

Project structure
phone-ticketing-fraud-detection/
├── notebooks/
│   └── Phone_Ticketing_Fraud_Detection.ipynb   -> full pipeline, tested end-to-end
├── data/
│   └── phone_ticketing_taps.csv                -> synthetic tap dataset (3,028 rows)
└── README.md
