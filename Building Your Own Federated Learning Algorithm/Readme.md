## **Algorithm**

1. Dataset
  *  Input dataset
  *  Group them in a set of `BATCH_SIZE`
  *  Divide the data among `NUM_CLIENTS`
2. Model
  *  Create a keras model for optimization at each client
  *  Wrap the keras model using `tff.learning.from_keras_model`. Specify loss and metrics for evaluation.
3. Client Update 
  *  `@tf.function`: 
      * Argument: model, dataset, server_weights, client optimizer
      * Assigns server weights to client weights
      * Performs optimization using dataset
      * Returns: Updated client weights
  * `@tff.tf_computation`:
      * Argument: dataset, server weights
      * Calls wrapped Keras model
      * Defines optimizer for clients
      * Returns: updated client weights
4. Server Update
  * `@tf.function`:
      * Argument: model, mean client weights
      * Assigns mean client weights to server weights
      * Returns: updated server weights
  * `@tff.tf_computation`:
      * Argument: mean client weights
      * Calls wrapped Keras model
      * Returns: updated server weights
5. Next
  * Argument: Server weights, federated dataset
  * Broadcasts server weigths to the clients
  * Calls client update function to update their weights
  * Computes mean of the updated client weights
  * Calls server update function to update its weight 
  * Returns: Updated server weights
6. Define an iteratice process usign `tff.templates.IterativeProcess` with next and initialization functions as argument.
