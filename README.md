This repository contains a comprehensive MATLAB simulation platform for evaluating and comparing advanced handover strategies in 5G mmWave networks, specifically designed for high-speed mobility scenarios like trains. The core of this project is to demonstrate the significant performance gains of an intelligent, AI-driven handover mechanism (Multi-Agent Q-Learning) when compared against traditional and simpler predictive algorithms.

The entire simulation, from environment modeling to final report generation, is contained within the `LSTM_Testing.m` script.

##  Environment 

The script constructs a detailed and realistic virtual world to test the handover algorithms under challenging conditions.

* **Network Type**: A 5G network operating in the **28 GHz mmWave** frequency band.
* **Geography**: A linear **10 km track** representing a high-speed railway, served by **20 Base Stations** (BSs) positioned every 500 meters.
* **Mobile Users**: **5 high-speed trains**, each moving at a constant velocity of **300 km/h**. 
* **Channel Realism**: The simulation doesn't just use ideal conditions. It incorporates crucial real-world channel effects:
    * **Path Loss & Shadow Fading**: Realistic signal degradation over distance and due to obstructions.
    * **Doppler Effect**: Signal distortion and degradation directly resulting from the trains' high velocity.
    * **Environmental Factors**: The simulation introduces periods of severe signal disruption to mimic **tunnels** or **adverse weather conditions**.

## Algorithms Compared

The simulation executes and evaluates three distinct handover decision algorithms in parallel to provide a clear performance comparison.

### 1. Traditional A3 Algorithm
A standard, reactive handover method. It triggers a handover only **after** a neighboring BS signal has been stronger than the serving BS by a fixed margin (`A3_offset`) for a specific duration (`Time-to-Trigger`). This method is reliable but often too slow for high-speed scenarios.

### 2. LSTM-Based Prediction
A proactive strategy that uses the **simulated output of an LSTM neural network** to predict future signal strength. It attempts to initiate a handover *before* the current connection degrades, aiming for a smoother transition. Note: To maintain focus on the handover logic, the script simulates an *imperfect* LSTM's output rather than training a full model.

### 3. Multi-Agent Q-Learning (Proposed Solution)
This is the most advanced, AI-driven approach. Each train acts as an intelligent "agent" that learns the optimal handover policy over time.

* **Actions**: At each step, the agent can choose to **Stay** with the current BS, initiate a **Handover** to a better BS, or establish **Dual Connectivity** for enhanced reliability.
* **Complex Reward Function**: The agent's learning is guided by a sophisticated reward system. It gets positive rewards for high **throughput** and stable **QoS**, but is penalized for the **cost of handovers**, high **network load**, and the negative impacts of the **Doppler effect**. This teaches the agent to make balanced decisions that optimize overall performance, not just signal strength.


## Key Features & Methodology

This simulation platform goes beyond a simple comparison and includes several advanced analytical stages:

* **Large-Scale Extrapolation**: It runs the detailed simulation on a small scale and then statistically **extrapolates the results** to model a larger network of 50 trains and 100 BSs, providing insights into scalability.
* **Multi-Scenario Analysis**: Tests the robustness of each algorithm against simulated network conditions like **Heavy Rain, Tunnels, Urban Canyons, and Network Congestion**.
* **Real-Time Adaptation**: Includes a module to simulate how the Q-Learning model can **adapt its strategy "on-the-fly"** when network conditions suddenly change, demonstrating its resilience.
* **Dataset Generation**: The script processes all simulated data into a rich, structured dataset that could be used to train a production-ready machine learning model for handover management.

## How to Run the Simulation

The source code is written in MATLAB. You must use the MATLAB environment to run the simulation.

### Prerequisites
* **MATLAB**: R2020a or newer is recommended. The Parallel Computing Toolbox is also recommended as the script will attempt to use it (`parpool`).
* **C/C++ Compiler**: Ensure you have a compiler configured with MATLAB (run `mex -setup` in MATLAB to check). While this script is pure `.m` code, this is good practice for MATLAB simulations.

### Execution Steps
1.  **Clone the Repository**:
    ```bash
    git clone [https://github.com/your-username/High-speed-handover-optimization-in-5G-using-Hybrid-LSTM-and-Q-Learning-Framework.git](https://github.com/your-username/High-speed-handover-optimization-in-5G-using-Hybrid-LSTM-and-Q-Learning-Framework.git)
    ```
2.  **Open MATLAB**: Launch MATLAB and use its file browser to navigate into the cloned repository folder.
3.  **Run the Script**: In the MATLAB Command Window, simply run the main file:
    ```matlab
    >> LSTM_Testing
    ```

---

## Expected Output

After running the script, you can expect the following:

1.  **Command Window Logs**: Detailed progress updates as the simulation executes its 15 distinct steps.
2.  **Generated Plots**: Several figure windows will appear, visualizing the results:
    * Throughput comparison between the three algorithms.
    * Performance analysis across different network scenarios.
    * A detailed plot of the Q-Learning agent's throughput and handover events over time.
    * A comparison of the adaptive vs. non-adaptive AI models. 
3.  **Final Report**: A summary table will be printed in the command window, presenting the final performance metrics (Handover Success Rate, Average Throughput, Latency, etc.) for each algorithm.
4.  **Saved Data**: A file named `high_speed_network_simulation_results.mat` will be created in the directory, containing all the data generated during the simulation for your own further analysis.








