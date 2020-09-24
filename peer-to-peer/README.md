# SHEMS
Smart home energy management system of a peer-to-peer network considering modulating heat pumps and photovoltaic systems
Explore the results interactively:   [![Binder](https://mybinder.org/badge_logo.svg)](https://mybinder.org/v2/gh/lilanger/PEERS/master?filepath=peer-to-peer%2FSHEMS_visualization_Interactive_julia.ipynb)

<p align="center">
  <img src="pics\PEERS_graph.png" width="400"/>
</p>

## Optimization model written in Julia JuMP
>Minimize net profits and comfort violations (base)
>  ``SHEMS_optimizer_peer.jl''


## How to run the model:
1) Run the file ``run_SHEMS.jl``  
2) Choose the combination of:     
  - time horizons
  - number  of peers
  - tariff case
  
  using function roll_SHEMS(market_flag, n_peers, n_market, h_start, h_end, h_predict, h_control, case)   
  * market_flag -> 0 = no P2P market, 1 = with P2P market  
  * n_peers -> 1 up to 5 peers (1=prosumager, 2=prosumer, more=consumer)  
  * n_market -> multiplier for market participants (e.g., for n_peers=3, n_market=1 gives 3, n_market=10 30 participants (10 each))  
  * h_start -> start of modeling horizon, standard = 1 (January 1 at 1 am)  
  * h_end -> end of modeling horizon, standard = 8760 (December 31 at 12 am)  
  * h_predict -> length of prediction horizon (full information)  
  * h_control -> length of control horizon (decision horizon)  
  * case ->   
    * case #1: current regime with FiT,   
    * case #2: current regime without FiT,   
    * case #3: proposed regime (w FiT),   
    * case #4: proposed regime (w/o FiT),   
    * case #5: area regime (w FiT),   
    * case #6: area regime (w/o FiT)  

### Examples:
Run model with 
  - whole year (1-8760h), prediction horizon 36h, control horizon 12h, 3 peers, case #1 (current regime, with FiT)
  >``roll_SHEMS(1, 3, 1, 1, 8760, 36, 12, 1)``

 
### Results .csv files in the result folder follow the name convention  
``$(date)_results_$(h_predict)_$(h_control)_$(h_start)-$(h_end)_$(market_flag)_$(n_peers)_$(case).csv``
