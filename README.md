# MOSFETS_DNN-PSO_Optimisation
Used a Deep Neural Network implemented on Keras framework to train the variables relating to arrangement of MOSFETS on an Integrated Circuit. Applied Particle Swarm Optimisation and Genetic Algorithms to get the arrangement with minimal delay and dissipation. Part of Mini Project in Summer'20

## ABSTRACT ##
Through Simulation softwares, the Delay and Leakage values for a Full Adder circuit of MOSFETs were computed for 50000 different Length
and Width parameters for all the 28 transistors. Using these values as training data, we created a Neural Net Model implemented on the
Keras framework to predict the delay and leakage values for unknown L and W parameters. Then we applied Genetic Algorithms and Particle
Swarm Optimisation techniques to find the best suitable 56 values (28 L and 28W) for which the Delay and Leakage values were the least.

## PROCEDURE ##
1. Read, understood and cleaned our data with popular data management library Pandas. The data was split 80:20 for training and testing.

2. Built the neural network model using Keras with Tensorflow backend. To build the Neural Net, Deep Learning was used. The Neural consisted of 9 layers. The input layer had 56 nodes. The hidden layers had 43, 35, 29, 25, 20, 26, and 12 nodes while the output layer had 6 nodes for the delay model and 1 node for the leakage model. All the layers but the last one used ReLu activation function and the last layer used a linear regressor
alone. Adam optimization technique was used to converge faster.

3. The two models were trained independently on data consisting of 40000 rows for delay and leakage values separately.

4. Both the models were tested using both R2 scores and MSE to get an idea of their performance on an unseen test set of 10000 rows.

5. We optimised our model parameters given initial sizing using genetic algorithms and particle swarm optimization. To do this the cost function was
defined such that it took into account both the delays and leakages. Hence both Neural nets were called simultaneously to provide the values for a test
set of 56 parameters.

6. Then the results were compared to initial sizing to find out the efficiency of the framework.

## MODEL
2 Models were built, one for Delay Values and the other for Leakage values.

Following is a detailed description of the Delay model.
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

optimised delays =

[5.592054597158835e-12, 1.1030185445570773e-11,
5.4595087131681375e-12, 1.3326664424773149e-11,
5.779232994940209e-12, 9.799409547706084e-12]

optimised leakage = 1.3509002e-06

### Genetic Algorithms
Genetic Algorithms converged to give good results as well.<br> The population size was 10. And 2 parents for each child population were chosen randomly from probabilistically weighted parents. The weights corresponded to the inverse of their fitness functions.<br>
The algorithm was allowed to converge for 1000 iterations.

## CONCLUSION ##
Achieved a model with R2 score 0.999 and was able to converge the model for delays and leakages. The trained Neural Net model had an average MSE of 2%. Both the algorithms Genetic and Particle Swarm Optimisation Technique were able to converge. The delay values reduced considerably by 34% as compared to the initial sizing and the leakage went up by only 8%. The inverse relation between the two parameters resulted in such a behaviour nevertheless this skewness of 34 versus 8 gives weight to the credibility of our proposed framework and further improvements could lead to even better results.

