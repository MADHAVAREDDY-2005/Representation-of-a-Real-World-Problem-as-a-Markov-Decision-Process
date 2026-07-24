# Representation-of-a-Real-World-Problem-as-a-Markov-Decision-Process


## Aim

To represent the real-world problem of selecting the best route from the hostel to the college as a Markov Decision Process (MDP) by defining its states, actions, transition probabilities, reward function, and Python representation.

---

## Problem Statement

A student travels from the hostel to the college every day and must choose the best route to reach the destination. Three routes are available: Straight Road, Guest House Road, and Canteen Road. The Straight Road is the fastest route, while the Guest House Road and Canteen Road may experience traffic, and a gate on these routes may sometimes be closed for vehicles. If the gate is closed, the student must continue by walking, which increases the travel time. This route selection process can be represented as a Markov Decision Process (MDP) because the student's next decision depends only on the current location and the selected route.

## Problem Description

Choosing the best route from the hostel to the college is a real-world sequential decision-making problem. Every day, the student begins the journey from the hostel and selects one of the three available routes to reach the college. The Straight Road usually provides the shortest travel time with minimal traffic. The Guest House Road and Canteen Road may have traffic congestion, and the gate on these routes may be either open or closed for vehicles. If the gate is open, the student can continue by vehicle. If the gate is closed, the student must park the vehicle and continue by walking, resulting in additional travel time.

This problem can be modeled as a Markov Decision Process (MDP), where the student acts as the agent, the different stages of the journey represent the states, the route choices and travel decisions represent the actions, and reaching the college quickly yields a higher reward, while delays caused by traffic or walking result in lower rewards. The process ends when the student successfully reaches the college.

---

## MDP Components

A Markov Decision Process is represented as:

$$
MDP = (S, A, P, R, \gamma)
$$

Where:

| Symbol | Meaning |
|---|---|
| $S$ | Set of states |
| $A$ | Set of actions |
| $P$ | Transition probability function |
| $R$ | Reward function |
| $\gamma$ | Discount factor |

---

## State Space

The state space consists of all possible situations that the student can experience while travelling from the hostel to the college.

```text
S = {
    S0: Hostel,
    S1: Straight Road,
    S2: Guest House Road,
    S3: Canteen Road,
    S4: Gate Open,
    S5: Gate Closed,
    S6: College
}
```


---

## Sample State

**S5: Gate Closed**

This state represents the situation where the student reaches the Guest House Road or Canteen Road and finds that the gate is closed for vehicles. As a result, the student cannot continue by vehicle and must walk to reach the college, which increases the travel time.

---

## Action Space

The action space consists of all possible actions that the student can take while travelling from the hostel to the college.

```text
A = {
    A1: Take Straight Road,
    A2: Take Guest House Road,
    A3: Take Canteen Road,
    A4: Continue by Vehicle,
    A5: Continue by Walk,
    A6: Reach College,
    A7: Stop
}
```


---

## Sample Action

**A1: Take Straight Road**

This action represents the student's decision to travel from the hostel to the college using the Straight Road. It is the fastest route with minimal traffic, allowing the student to reach the college in the shortest time and receive the highest reward.


---

## Transition Probability

The transition probability defines the likelihood of moving from one state to another after the student chooses a particular action. In this problem, the next state depends on the selected route and the condition of the gate. The Straight Road always leads directly to the college, while the Guest House Road and Canteen Road may have either an open or closed gate.

General form:

$$
P(s' \mid s,a)
$$

where:

- $s$ = Current state
- $a$ = Action taken
- $s'$ = Next state

The transition probabilities for this MDP are:

| Current State | Action | Next State | Probability |
|---------------|--------|------------|-------------|
| Hostel (S0) | Take Straight Road | Straight Road (S1) | 1.0 |
| Hostel (S0) | Take Guest House Road | Guest House Road (S2) | 1.0 |
| Hostel (S0) | Take Canteen Road | Canteen Road (S3) | 1.0 |
| Guest House Road (S2) | Continue Journey | Gate Open (S4) | 0.8 |
| Guest House Road (S2) | Continue Journey | Gate Closed (S5) | 0.2 |
| Canteen Road (S3) | Continue Journey | Gate Open (S4) | 0.6 |
| Canteen Road (S3) | Continue Journey | Gate Closed (S5) | 0.4 |
| Straight Road (S1) | Reach College | College (S6) | 1.0 |
| Gate Open (S4) | Continue by Vehicle | College (S6) | 1.0 |
| Gate Closed (S5) | Continue by Walk | College (S6) | 1.0 |

---

## Reward Function

The reward function provides feedback to the student (agent) after taking an action and moving from one state to another. Routes that help the student reach the college quickly receive higher rewards, while delays caused by traffic or walking due to a closed gate receive lower or negative rewards.

General form:

$$
R(s,a,s')
$$

The reward values for this MDP are:

| Current State | Action | Next State | Reward |
|---------------|--------|------------|--------|
| Hostel (S0) | Take Straight Road | Straight Road (S1) | +10 |
| Hostel (S0) | Take Guest House Road | Guest House Road (S2) | +6 |
| Hostel (S0) | Take Canteen Road | Canteen Road (S3) | +4 |
| Guest House Road (S2) | Continue by Vehicle | Gate Open (S4) | +5 |
| Guest House Road (S2) | Continue by Walk | Gate Closed (S5) | -3 |
| Canteen Road (S3) | Continue by Vehicle | Gate Open (S4) | +3 |
| Canteen Road (S3) | Continue by Walk | Gate Closed (S5) | -5 |
| Straight Road (S1) | Reach College | College (S6) | +10 |
| Gate Open (S4) | Continue by Vehicle | College (S6) | +8 |
| Gate Closed (S5) | Continue by Walk | College (S6) | +4 |

---

## Graphical Representation

<img width="1536" height="1024" alt="image" src="https://github.com/user-attachments/assets/f63b5a5b-9e19-4916-b9b0-52c3b17454f7" />


---

## Python Representation

```python
from pprint import pprint

print("Name: K MADHAVA REDDY")
print("Register Number: 212223240064")

P = {

    "Hostel": {

        "Take Straight Road": [
            (1.0, "Straight Road", 10, False)
        ],

        "Take Guest House Road": [
            (1.0, "Guest House Road", 6, False)
        ],

        "Take Canteen Road": [
            (1.0, "Canteen Road", 4, False)
        ]
    },

    "Straight Road": {

        "Reach College": [
            (1.0, "College", 10, True)
        ]
    },

    "Guest House Road": {

        "Continue by Vehicle": [
            (0.8, "Gate Open", 5, False)
        ],

        "Continue by Walk": [
            (0.2, "Gate Closed", -3, False)
        ]
    },

    "Canteen Road": {

        "Continue by Vehicle": [
            (0.6, "Gate Open", 3, False)
        ],

        "Continue by Walk": [
            (0.4, "Gate Closed", -5, False)
        ]
    },

    "Gate Open": {

        "Continue by Vehicle": [
            (1.0, "College", 8, True)
        ]
    },

    "Gate Closed": {

        "Continue by Walk": [
            (1.0, "College", 4, True)
        ]
    },

    "College": {

        "Stop": [
            (1.0, "College", 0, True)
        ]
    }
}

print("\nMDP Representation (P):\n")
pprint(P, width=100)
```
---
## Output

<img width="867" height="355" alt="image" src="https://github.com/user-attachments/assets/bbb648b5-9c20-4b2e-9adb-8630c720fbc6" />


---

## Result

Thus, the Hostel to College Route Selection problem was successfully modeled as a Markov Decision Process (MDP) and implemented in Python, demonstrating the states, actions, transition probabilities, reward function, and terminal state involved in selecting the optimal route to reach the college.


---

