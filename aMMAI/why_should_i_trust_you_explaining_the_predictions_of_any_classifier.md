# “Why Should I Trust You?” Explaining the Predictions of Any Classifier


## Introduction

Despite widespread adoption, machine learning models remain mostly black boxes. Ubderstanding why the prediction is made is quite important for human user to trust the model, especially in some applications where reasoning might be crucial. In this paper, they proposed **LIME**, a novel explanation technique that explains prediction of any classifier in an interpretable and faithful manner, by learning an interpretable model locally around the prediction.

## Method

1. *Characteristics for explainers*
- Interpretable
- Local fidelity
- Model-agnostic
- Global perspective

2. *Local Intepretable Model-Agnostic Explanations*
- Interpretable Data Representations: binary vector for text, super-pixel for image
- Fidelity-Interpretability Trade-off: minimize faithfulness (fidelity) and complexity of explanation (interpretability) together
- Sampling for Local Exploration: sample locally for local-aware explanations
- Sparse Linear Explanations
- Submodular Pick for Explaining Models: select predictions that carries the most information

## Results

1. *Are explanations faithful to the model?*
- Measure faithfulness with recall of *gold* set of features
- **LIME** consistently provides pver 90% recall
2. *Should I trust this prediction?*
- Select 25% "untrustworthy" features randomly
- Label predictions as "untrustworthy" if prediction changes when "untrustworthy" features are removed, and "trustworthy" otherwise
- Simulate user with a similar manner using the linear approximated
- **LIME** dominates all other methods
3. *Can I trust this model?*
- Add noisy features and train competing models with similar validation accuracy but different test accuracy
- Select model with fewer untrustworthy explanation
- **LIME** outperforms other methods
4. *Can users select the best classifier?*
- Evaluate if users could select better model with explanation
- All methods are good at identifying the better model, where **LINE** with submodular pick outperforms other methods
5. *Can non-experts improve a classifier?*
- Select features according to explanations
- The model is improved after unimportant feature are removed
6. *Do explanations lead to insights?*
- Train an easy task (Husky vs. Wolf) and make the model predict according to backgroud (snow)
- Model is trusted by more than a third subjects before explanation is observed, and after explanation is observed, alsmost all subjects identified the correct insight

## Discussion

1. Explaining black-box models provide very important informations for human to make decisions (whether to trust  the prediction or not), with explanations, we could even improve the model by giving the model correct insights
2. The experiment of *Can non-experts improve a classifier?* feels like online learning to me, but is directly performed on features rather than on data, which might be more effective
3. The paper experimented mostly on small and simple models, I wonder if it still performs well with more complex models that might not be easy to explain
4. The human subjects evaluation is something that is not often seen, the results were very interesting and how to design such experiment for evaluation is also quite fresh to me