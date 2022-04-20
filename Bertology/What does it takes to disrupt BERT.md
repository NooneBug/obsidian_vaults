Based on the paper: [BERT Busters: Outlier Dimensions that Disrupt Transformers](http s://text-machine-lab.github.io/blog/2021/busters/) 

You can 'kill' BERT by disabling <0.0001% of model weights, experimented on 6 versions of BERT + XLNet, BART, ELECTRA & GPT-2

It was observed that some high-magnitude weights are in the same position in the final operation across transformer layers (final operation: LayerNorm in BERT & co, dense layer in GPT-2), (weights are: scaling factors and biases in BERT & com outputs in GPT-2)

By disabling these weights ROBERTA performance in filling the gaps are terrible, if the same number of weights and biases are randomly disabled, the performance are still good
