## **Algorithm**

1. **Dataset**
  * Input dataset
  * Preprocess by shuffling, dividing in batches and flattening.
  * Federated dataset
    * Argument: Client data, client IDs 
    * Creates list of dataset for the selected client IDs
2. **Client Selection**
3. Model
  * Keras model
  * Wrapping Keras model
4. Defining iterative process using `tff.learning.build_federated_averaging_process`
5. Initialize iterative process
6. Training over multiple federated averaging process

### **Customizing model implementation**

1. Creating variables
2. Forward pass
  * Arguments: varables, batch
  * Compute predictions
  * Compute model loss
  * Compute accuracy
  * Update variables
  * Returns: Loss, predictions
3. Aggregating local metrics
4. Model
  * Call variable creating function, define trainable, non trainable and local variables
  * Define forward pass function
    * Arguments: self, batch
    * Computes loass and prediction on batch using self variables
    * Returns: batch output using `tff.learning.BatchOutput`
  * Define local metric function
    * Arguments: self
    * Returns: local metrics for self variables
  * Define federatedoutput computation to aggregrate metrics across clients.
5. Defining iterative process using `tff.learning.build_federated_averaging_process` and the above defined model
6. Initialize iterative process
7. Training over multiple federated averaging process 
8. Evaluate model using `tff.learning.build_federated_evaluation`
