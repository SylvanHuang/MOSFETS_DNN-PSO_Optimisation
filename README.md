# MOSFETS_DNN-PSO_Optimisation
Used a Deep Neural Network implemented on Keras framework to train the variables relating to arrangement of MOSFETS on an Integrated Circuit. Applied Particle Swarm Optimisation and Genetic Algorithms to get the arrangement with minimal delay and dissipation. Part of Mini Project in Summer'20

## MODEL

I tried a Deep Neural Net using Keras and got a R2 score of 0.9997 for both train and test. ( I did an 80, 20 split for train and test)

The NN has 1 input layer, 4 hidden layers and 1 output layer.

Input layer - 56 nodes<br>
Hidden Layer1 - 43 nodes, ReLu activation ( I tried Leaky ReLu as well, it tends to perform better in general cases but here ReLu seemed to perform better)<br>
Hidden Layer2 - 35 nodes, ReLu activation<br>
Hidden Layer3 - 29 nodes, ReLu activation<br>
Hidden Layer4 - 25 nodes, ReLu activation<br>
Output Layer - 6 nodes, Linear activation ( as it is a regression model)<br>

I have used Adam optimisation technique ( I tried with SGD as well, but as expected Adam performed better) and let the model train for 1000 epochs.

The average train error is 1.83% and average test error is 1.87%.

## OPTIMISATION

### Particle Swarm Optimisation
Then I used Particle Swarm Optimisation algorithm using both PySwarms and a manual code. The results from PySwarms were better. I chose the sum of all 6 delays as the fitness function for the algorithm. I had run this optimisation 10 times for 500 iterations each and stored the best results. 

The social best parameter of 0.3, individual best hyperparameter of 0.5, and an inertia of 0.9 were used.

The 6 delay values for the best result are the following:
[2.8448270e-11, 2.1319639e-11, 2.9405155e-11, 3.9711571e-11, 3.9871099e-11, 3.5339159e-11]

### Genetic Algorithms
Genetic Algorithms converged to give good results as well.<br> The population size was 10. And 2 parents for each child population were chosen randomly from probabilistically weighted parents. The weights corresponded to the inverse of their fitness functions.<br>
The algorithm was allowed to converge for 1000 iterations.
