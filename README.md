# CPU Scheduling Simulator

An experiment comparing four CPU scheduling algorithms (**FCFS, SJF, Priority and MLFQ**) using a course-provided multithreaded **Java** simulation ("Allegra the Barman", where drink orders play the role of processes), plus a **Weighted Fair Queue** scheduler I designed.

The base simulation was supplied by the course. My work, which is what this repo contains, was the data collection, the experiment automation, the analysis and the WFQ extension.

## Results
- Automated **200 controlled experiments** (4 schedulers × 5 random seeds × 10 load levels) with a Bash script, producing **49,208 order records**
- Analysed in Python across 10 graphs (box plots, mean/median trends, throughput, fairness, worst-case waits)
- **SJF** cut mean waiting time by **29%** versus FCFS (and median by ~49×), but caused starvation, with some orders waiting more than 20 seconds
- Data-integrity checks found **zero violations** across all records

## Bonus: Weighted Fair Queue
Each order's score is `execution time − 0.3 × time waited`. Short orders still go first like SJF, but long-waiting orders climb the queue until they are served, so nothing starves.

## What's in this repo
| File | What I wrote |
|---|---|
| `recordCompletedOrder` (excerpt of `Barman.java`) | Logs every completed order with waiting, response and turnaround times to CSV |
| `run_experiments.sh` | Runs all 200 scheduler × seed × load combinations |
| `analyse_results.py` | Loads the CSVs and produces the 10 graphs |
| `bonus_implementation/` | The Weighted Fair Queue scheduler |
| `graphs/` | Result figures |

*Built for an Operating Systems course at the University of Cape Town (2026).*

> **To finish this repo:** add only the parts you wrote: your `recordCompletedOrder()` method, `run_experiments.sh`, `analyse_results.py`, your WFQ code and the graphs. Leave out the course's starter code, since it isn't yours to publish.
