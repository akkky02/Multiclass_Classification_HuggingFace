# Multi-Class Classification Model Comparison

This Jupyter notebook experiments with different pre-trained models for a multi-class text classification task.

## Models Compared

- DistilBERT
- DistilRoBERTa
- Giganticode BERT model pre-trained on Stack Overflow comments

## Dataset

The dataset used is a custom multi-class classification dataset loaded from a CSV file. It has 10 balanced classes.

## Training Procedure 

- The dataset is loaded and split into train, validation, and test sets
- Small balanced subsets are created for faster experimentation 
- Models are initialized with model-specific configurations
- Models are trained for 2 epochs with a batch size of 16
- Evaluation is performed at regular intervals using accuracy and F1 macro
- Training metrics and confusion matrices are logged 

## Key Functions

- `load_custom_dataset`: Loads dataset from CSV
- `split_dataset`: Splits loaded dataset into subsets
- `get_small_balanced_subset`: Creates a small balanced sample of the dataset 
- `get_tokenized_dataset`: Tokenizes text using model-specific tokenizer
- `setup_dataset`: Overall dataset preparation workflow  
- `initialize_model`: Initializes model, config and tokenizer 
- `compute_metrics`: Evaluation metrics computation  
- `get_trainer`: Sets up trainer object for training loop
- `log_and_plot_confusion_matrix`: Logs confusion matrix to W&B and plots
- `tokenize_train_evaluate_log`: Main train/eval loop

## Experiments

The notebook runs 3 experiments training the models on a small 200 sample/class balanced subset. Performance and training metrics are reported.


## Conclusion

The main findings from the notebook experiments are:

- The DistilBERT model achieved the lowest validation accuracy of 0.804 among the 3 models. Being a distilled version of BERT, it trades some performance for efficiency.

- The DistilRoBERTa model performed slightly better than DistilBERT, achieving a validation accuracy of 0.8505. As a distilled variant of RoBERTa architecture, it offers a good speed vs accuracy tradeoff.

- The giganticode/bert-base-StackOverflow-comments_2M model performed the best with a validation accuracy of 0.8635. Pre-training on in-domain Stack Overflow data likely helped this model achieve the highest accuracy.

In summary, the choice of pre-trained model significantly impacts multi-class classification performance. The giganticode BERT model specifically fine-tuned on relevant Stack Overflow data performed the best by leveraging in-domain knowledge.

However, smaller distilled models can reach comparable performance with lower computational requirements. The exact model chosen depends on the use case constraints around accuracy, model complexity, and inference speed.