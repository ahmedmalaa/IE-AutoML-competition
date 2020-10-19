# The Inspiration Exchange AutoML Competition

This repository provides instructions for participants engaging in the *Inspiration Exchange AutoML Competition* organized by the [vanderschaar lab](https://www.vanderschaar-lab.com/engagement-sessions/). Participation in this competition is open for all attendees of the vanderschaar lab Inspiration Exchange (IE) sessions (Check this [link](https://www.vanderschaar-lab.com/engagement-sessions/) for more information on how to join). The competition will take place as part of the third IE session held by our lab. The deadline for submitting the deliverables of the competition is November 5 at 16:00 GMT. Below are the description of the competition and instructions on how to join. 

## Robustness of AutoML to dataset shifts

Generalization performance of machine learning models is significantly affected by distributional mismatches between training and testing data. The sources for these distributional shifts vary depending on the application: the process being modeled may change over time, or the source of the training data may not be representative of the environment in which a model would be deployed. Designing machine learning models that are robust to distributional shift, e.g., models that are trained to work well even if the distribution of testing data differs from training data, is a key objective in many applications. 

In the first [two IE sessions](https://www.vanderschaar-lab.com/engagement-sessions/inspiration-exchange/), we discussed various automated machine learning (AutoML) algorithms that our lab has developed over the past few years. These algorithms are designed to automate modeling choices for the data set at hand, but they assume that training and testing data come from the same distribution. *The goal of this competition is to modify and amend one of our AutoML algorithms so that it becomes robust to distributional shifts*. The algorithm involved in the competition is [AutoPrognosis](http://proceedings.mlr.press/v80/alaa18b/alaa18b-supp.pdf), a system that automates ML pipelines using an advanced Bayesian optimization technique. Prof. van der Schaar has given a number of talks explaining the operation of AutoPrognosis; check her [talk](https://www.youtube.com/watch?v=d1uEATa0qIo) at the Alan Turing Institute for more details.  


## Instructions for particpating in the IE AutoML competition

### Overview and requirements

Participants are asked to modify the source code for AutoPrognosis to make it robust to distributional shift. Participants are provided with a training data set for binary classification, with features $X$ and binary labels $Y$. The features $X$ in the training data follow a certain distribution $P(X)$. Each participants will apply their modified AutoPrognosis to train a model that is "insensitive" to changes in $P(X)$ and submit their trained models to us. We will then test the submitted models on a number of testing sets (not accessible to participants ahead of time), each with a perturbed feature distribution $P\prime(X)$, and average the models' performance scores over these perturbed testing sets. The winning model will be the one with the highest average accuracy over the perturbed testing sets.

### Software

Participants are required to use the AutoPrognosis software from this [repository](https://github.com/ahmedmalaa/AutoPrognosis).

Installation instructions can be found [here](https://github.com/ahmedmalaa/AutoPrognosis/blob/master/doc/install.md).

To modify AutoPrognosis, you can simply come up with a different objective function for the Bayesian optimization algorithm. This can be done by modifying line 345 in [model.py](https://github.com/ahmedmalaa/AutoPrognosis/blob/master/alg/autoprognosis/model.py), i.e.,

```
rval_eva = evaluate_clf(X_in.copy(), Y_in.copy(), copy.deepcopy(modraw_), n_folds = self.CV)
```

You will need to come up with an alternative implementation of *evaluate_clf* that makes it invariant to the distribution of *X_in*. You are also free to follow a different approach to change the AutoPrognosis algorithm in order to fulfill the distributional robustness objectives, but note that other solutions may require a more involved engagement with the code and hence more time.


### Data

The training data is a public data set for elective general surgical patients at the Cleveland Clinic between January 2005 and September 2010. You can access the data from the [data](https://github.com/ahmedmalaa/IE-AutoML-competition/tree/main/data) folder in this repo. 

The data dictionary can be found [here](https://www.causeweb.org/tshs/datasets/Surgery%20Timing%20Data%20Dictionary.pdf).
Description for the clinical background of this data set can be found [here](https://www.causeweb.org/tshs/datasets/Surgery%20Timing%20Data%20Dictionary.pdf). 

### Code and model submission

Please submit the following by November 5 at 16:00 GMT:

- A trained AutoPrognosis model saved using the [pickle] library.
- Your modified code snippets or a link to the Github repo with the modified code.
- A 1- or 2-slide PPT presentation explaining the idea you implemented to improve AutoPrognosis' robustness to distributional shift. 

Please send these deliverables to both: ahmedmalaa@ucla.edu and nm736@cam.ac.uk 


### Competition winners

The winner will be announced and acknowledged on the vanderschaar lab website and will receive a signed certificate from Prof. van der Schaar acknowledging their achievement.


