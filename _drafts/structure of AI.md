---
published: false
---


Transformer is an encoder-decoder architecture. 
https://en.wikipedia.org/wiki/Transformer_(machine_learning_model)

 The encoder consists of a set of encoding layers that processes the input iteratively one layer after another and the decoder consists of a set of decoding layers that does the same thing to the output of the encoder.

The function of each encoder layer is to process its input to generate encodings, containing information about which parts of the inputs are relevant to each other. It passes its set of encodings to the next encoder layer as inputs. Each decoder layer does the opposite, taking all the encodings and processes them, using their incorporated contextual information to generate an output sequence.


Transformers typically undergo semi-supervised learning involving unsupervised pretraining followed by supervised fine-tuning.



U-Net
https://en.wikipedia.org/wiki/U-Net

The main idea is to supplement a usual contracting network by successive layers, where pooling operations are replaced by upsampling operators. Hence these layers increase the resolution of the output. What's more, a successive convolutional layer can then learn to assemble a precise output based on this information.[1]

One important modification in U-Net is that there are a large number of feature channels in the upsampling part, which allow the network to propagate context information to higher resolution layers.




