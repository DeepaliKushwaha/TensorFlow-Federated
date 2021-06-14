## **Algorithm**

1. Dataset
  * Input dataset
  * Get data for each digit and use digit as clients. Create a federated dataset
2. Define batch and model specification as ordered dictionary.
3. Forward pass function computing loss. Batch loss function return loss.
4. Initailization of model parameters.
5. Gradient descent on single batch:
  * Argument: inital model, batch,, learning rate
  * Define model variables
  * Define optimizer to be used
  * Train on one batch:
      * Parameters: madel variables, batch
      * Compute gradient
      * Apply grdients
      * Return updated parameters
  * Returns updated parameter trained on single batch
6. Gradient descent on sequence of data
  * Arguments: Initial model, learning rate, all batches to be used for training
  * Calls function to train one batch
  * Recursively uses all the batches to train the model
  * Returns: model parameters
7. Federated Evaluation
  * Arguments: model, data
  * Nroadcasts model from server to clients
  * Finds local loss
  * Returns mean of local losses
8. Federated Training
  * Arguments: model, learning rate, data
  * Broadcasts model and learning rates to clients
  * Trains the broadcasted model on each client
  * Returns mean of the updated parameters
9. Initialize mode, learning rate and train federated model over some iterations. 
