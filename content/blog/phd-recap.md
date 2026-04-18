---
title: "PhD Recap"
date: 2025-06-30T08:00:00+02:00
draft: false
summary: "I reflect on my own PhD journey and share how much doctoral experiences can differ in their structure, responsibilities, and focus."
categories: []
# custom_css: ["education-blog.css"]
---

## Every PhD Is Different

I recently completed my PhD (Dr.-Ing.) in Germany successfully. Earning it was demanding and at times exhausting, but it was also one of the most educational periods of my life. During my whole time as a PhD student, I became increasingly aware of how different doctoral paths can be. Of course, a doctorate in law differs greatly from one in the natural sciences or engineering, like the one I completed. That part never surprised me. What did surprise me was how much PhD experiences can differ even within the same field and at the same university. Over the years, I came to one simple conclusion: every PhD is different. 

## My PhD - a Breath of Diverse Tasks and Responsibilities

When [agent skills](https://platform.claude.com/docs/en/agents-and-tools/agent-skills/overview) were first proposed and released by Anthropic, I was initially skeptical about their use case. I didn't really
get the appeal of [MCPs](https://platform.claude.com/docs/en/agents-and-tools/mcp-connector) previously and was ready to dismiss skills similarly. Only a few weeks ago, I revisited agent skills
since I got annoyed by the tedious management of my ML-training runs via slurm. I always had to check if I used the correct
run ID, whether the requested dataloader workers and CPUs matched, and so on. Instead, I created a skill with all the explanations about
my slurm scripts, our GPU cluster and my output folder structure. I can now just point Claude Code to a previous run and ask it for a new run with X changed parameters.
This skill keeps me from insanity, but other than that, I don't really save much time.

However, after this skill worked better than expected, I tried to automate two more complex tasks.

1. Training run evaluation
2. Numerical simulation evaluation and tuning

## Training Run Evaluation

Since I am logging all ML experiments to WandB anyway, I usually have a good overview of what is happening during a run.
Additional health logs show loss spikes and gradient issues. But still, after creating a skill (including two scripts to fetch WandB data),
I now routinely point Claude at a recent run and let it analyze the run. This not only saves time but sometimes also catches issues faster
or analyzes things in more detail than I would. Claude looks at logs and loss curves, but also eval images or text.
For instance, for a physics-VAE model I am working on, Claude is surprisingly good at understanding the generated images and identifying a drop in quality.
It can identify posterior collapse, learning rates that are too high, and other training issues.

Right now, I am severely GPU-limited, so this does not speed up my research significantly, but with 100x the resources,
I am pretty sure I could point the agent towards a specific goal and let it do some iterations of hyperparameter tuning before checking in again.

## Running PDE Simulations for me

The most interesting skill I got working is running numerical simulations, analyzing the results and tweaking the parameters. Again, Claude is
actually smart enough to understand visual results and logs and tweak parameters to achieve the desired simulation results.
I am currently running [agent teams](https://code.claude.com/docs/en/agent-teams) in a codebase designed to generate a large variety of PDE simulations (training data for LLMs / physics models).
Teams of up to 20 agents run and analyze PDE simulations, change parameters, fix unstable simulations and produce up to 200 distinct simulation trajectories in a couple of hours.
This actually saves a significant chunk of my time. After all simulations finish, I generate an HTML report with GIFs and information from all simulations and then I point out simulations that seem wrong.
The next team can then focus on fixing these simulations.
The next step will be a detailed analysis script that the agents run, generating reports about energy/momentum conservation or other health checks.

## Issues and Future

Claude Code and other models are still LAZY; it is unbelievable (maybe Codex is better—I should investigate).
If not explicitly told—and checked upon—they sometimes skip issues
or alter values. For example, Claude sometimes changes simulation parameters to speed up the simulation, obviously altering
the outcome. They also miss video understanding and their image understanding sometimes misses details.

On the other hand, I am confident that current models can already do some tedious parts of an ML scientist's daily research.
Creativity and novelty might still be missing, but hyperparameter tuning or architecture tweaking is already possible.
I am excited about the new generation of models!