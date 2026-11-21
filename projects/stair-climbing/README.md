# Reinforcement-Learning-Based Stair Climbing on Unitree G1

## Overview

This project involved developing and evaluating a blind reinforcement-learning locomotion policy that enabled a waist-locked Unitree G1 humanoid robot to climb ordinary building stairs. The work progressed from simulation-based training through MuJoCo simulation-to-simulation testing to physical robot deployment.

The physical demonstration used the robot with Inspire RH56DFTP hands attached. The robot successfully climbed six stairs across approximately three to four test runs.

## Objective

Develop a locomotion policy for forward stair ascent on the Unitree G1. The stair-climbing method was not prescribed in advance.

## My contributions

Within a collaborative research effort and with mentor guidance, my work included:

- Replicating the Unitree G1 29-DoF model and waist-lock model for the training workflow.
- Working with the existing pyramid-stairs training environment.
- Training a blind stair-climbing policy.
- Evaluating policies and carrying out fine-tuning.
- Testing the policy in MuJoCo as a simulation-to-simulation validation step.
- Deploying the policy on the physical Unitree G1.
- Progressively testing on bricks and smaller obstacles before testing on ordinary building stairs.
- Observing and documenting failure modes during physical evaluation.

Physical testing was conducted with assistance from the team.

## Technical approach

The work used a simulation-first reinforcement-learning workflow. A policy was trained in the existing pyramid-stairs environment and evaluated in simulation. Candidate policies were then tested in MuJoCo before deployment on the physical humanoid.

The policy was blind in the sense that the locomotion policy relied on proprioceptive observations rather than visual stair perception.

**Frameworks and platforms identified during the work:**

- Unitree RL Lab
- NVIDIA Isaac Lab
- RSL-RL (the training/playback workflow used this library; the exact algorithm configuration for the customised task has not yet been independently confirmed)
- MuJoCo
- Unitree G1, 29-DoF configuration

## Engineering challenges

### Waist-locked locomotion

The most difficult part was obtaining useful stair-climbing behaviour on the physical robot with a waist-locked configuration. Several earlier policies trained for roughly 10,000–15,000 iterations were discarded because they produced unsuitable posture, insufficient leg lift, or inadequate stride length.

The policy also had to operate with the mass of the Inspire RH56DFTP hands accounted for. The hands remained attached during physical testing, and the robot climbed the stairs in that configuration.

### Environment-induced directional bias

The training used the existing pyramid-stairs environment rather than a custom stair environment. Its stair surfaces were relatively wide. During training, the robot developed a rightward drift as part of its learned climbing behaviour, and rightward drift was also observed during physical stair ascent.

This is documented as an observed behaviour associated with the training environment; the precise causal mechanism has not been isolated.

## Evaluation and results

### Simulation

The policy demonstrated stair climbing in simulation before physical deployment. MuJoCo was used for simulation-to-simulation testing.

### Physical testing

| Attribute | Observation |
|---|---|
| Robot | Unitree G1, 29-DoF |
| Waist configuration | Waist-locked |
| Attached hardware | Inspire RH56DFTP hands |
| Test stairs | Ordinary building stairs |
| Approximate stair height | 15–17 cm |
| Approximate stair width | 80–100 cm (estimated) |
| Demonstrated ascent | Six stairs |
| Number of successful runs reported | Approximately 3–4 |

These are reported demonstration results, not a statistically established success rate or a claim of robust performance across varied stair geometries.

## Observed limitations

- The policy was less effective on stairs with narrower treads.
- Rightward drift occurred during stair ascent.
- The policy supported forward stair climbing; sideways and backward stair navigation were not demonstrated.
- The learned gait produced heavy steps on flat ground.
- Switching from the stair policy to the built-in walking controller during operation caused the robot to enter damping mode and fall. As a result, movement between locations and transitions between locomotion modes were difficult.

## Future directions

A proposed next step was to train a separate navigation/locomotion policy and investigate safe transitions between policies, allowing the robot to use different behaviours for stair ascent and general navigation. This remained a proposed direction and was not completed as part of the reported demonstration.

Other potential investigation areas include evaluating varied stair widths, reducing directional drift, improving flat-ground gait quality, and designing a validated policy-transition procedure.

## Scope and disclosure

This case study is a high-level description of work performed in a collaborative research setting. It deliberately excludes source code, model weights, internal configuration values, deployment implementation details, and non-public research artefacts. It should be shared publicly only to the extent permitted by the relevant institution and project supervisors.

## Accuracy notes

- The stair environment was the existing pyramid-stairs environment, not a custom-built environment.
- The physical result reported here is six stairs across approximately three to four runs.
- The approximate stair dimensions are estimates, not measured specifications.
- PPO is not asserted as a confirmed algorithm for the customised stair task; the exact training configuration has not yet been verified.
