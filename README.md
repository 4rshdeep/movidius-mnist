## movidius-mnist

Run the code in `python3 mnist_deep.py` to train the network and make sure saver.save() is called to save the trained network. After the program completes, if it was successful, saver.save() will have created the following files:

    mnist_model.index
    mnist_model.data-00000-of-00001
    mnist_model.meta
    
Remove training specific code from the network, and add code to read in the previously saved network to create an inference only version. For this step its advised that you copy the original TensorFlow™ code to a new file and modify the new file. For example if you are working with mnist_deep.py you could copy that to mnist_deep_inference.py. Things to remove from the inference code are:

    Dropout layers
    Training specific code
        Reading or importing training and testing data
        Cross entropy/accuracy code
        Placeholders except the input tensor.

Run the inference version of the code to save a session that is suitable for compiling via the ncsdk compiler. This will only take a second since its not actually training the network, just re-saving it in an NCS-friendly way. After you run, if successful, the following files will be created.

    mnist_inference.index
    mnist_inference.data-00000-of-00001
    mnist_inference.meta
    
Compile the final saved network with the following command and if it all works you should see the mnist_inference.graph file created in the current directory. Note you pass in only the weights file prefix “mnist_inference” for the -w option for a TensorFlow™ network on the compile command line. The full command is below.
```mvNCCompile mnist_inference.meta -s 12 -in input -on output -o mnist_inference.graph```
