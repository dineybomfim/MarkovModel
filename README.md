# MarkovModel

[![Build Status](https://travis-ci.org/dineybomfim/MarkovModel.svg?branch=master)](https://travis-ci.org/Alamofire/Alamofire)
[![codecov](https://codecov.io/gh/dineybomfim/MarkovModel/branch/master/graph/badge.svg)](https://codecov.io/gh/dineybomfim/MarkovModel)
![POD](https://img.shields.io/badge/swift-4.1-red.svg)
<!--
[![CocoaPods](https://img.shields.io/cocoapods/at/MarkovModel.svg)]()
[![CocoaPods](https://img.shields.io/cocoapods/dt/MarkovModel.svg?label=pod-downloads)]()
[![CocoaPods Compatible](https://img.shields.io/cocoapods/v/MarkovModel.svg)](https://img.shields.io/cocoapods/v/MarkovModel.svg)
[![Platform](https://img.shields.io/cocoapods/p/MarkovModel.svg?style=flat)](https://markovmodel.github.io/MarkovModel)-->
[![codebeat badge](https://codebeat.co/badges/366a5994-abec-4c41-8e64-6f71ff9eab33)](https://codebeat.co/projects/github-com-dineybomfim-markovmodel-master)

# Description
**MarkovModel** is a framework for ... `make an introduction for this component. Explaining the major business goals.`
https://en.wikipedia.org/wiki/Markov_model
Markov models
System state is fully observable

**Features**

- [x] Automatically creates Markov Chain based on a given sequence of transactions;
- [x] Allows manual matrix manipulation for mutating members;
- [x] Markov decision process with weighted random selection;
- [x] Next state prediction.

# Installation

#### CocoaPods:
[CocoaPods](https://guides.cocoapods.org/using/getting-started.html) is a dependency manager for Cocoa projects. You can get more information about how to use it on [Using CocoaPods](https://guides.cocoapods.org/using/using-cocoapods.html)

Once you ready with CocoaPods, use this code in your `Podfile`:

```
pod 'MarkovModel'
```

# Requirements
Version | Language | Xcode | iOS
------- | -------- | ----- | ---
 1.0.0  | Swift 4.1  |  9.0  | 10.0

# Programming Guide
The Markov Model can be used to achieve many goals. This section will explain the usage while providing some possible scenarios.

* Traning the Model
* Decision Process
* Debugging

#### Training the Model
Start by importing the package in the file you want to use it. There are two options of working with the model. By instantiating or by traning it statically.

```
import MarkovModel
...
let markovModel = MarkovModel(transitions: ["A", "B", "C", "A", "C"])
```

For very large amount of data (transitions), you may rather take the static approach, once it can train the model and work on it all at once in a closure.

```
import MarkovModel
...
MarkovModel.process(transitions: ["A", "B", "C", "A", "C"]) { model in
	// perform the operations on model
}
```

#### Decision Process
For performance and better API design, all the Markov Decision Process algorithms are done in the matrix itself.
You can calculate any future state by calling `next`. There are 3 possible decision process options: `predict`, `random` and `weightedRandom`.

```
markovModel.chain.next(given: "B", process: .random)
```

You can ommit the process parameter and the default option will be `predict`.


```
markovModel.chain.next(given: "B")
```

Sometimes you may want to some column of the matrix itself. The method `probabilities` can be used to retrieve all the possible transitions from a given state.

```
markovModel.chain.probabilities(given: "B")
```
#### Decision Process
For performance and better API design, all the Markov Decision Process algorithms are done in the matrix itself.
You can calculate any future state by calling `next`. There are 3 possible decision process options: `predict`, `random` and `weightedRandom`.

```
let markovModel = MarkovModel(transitions: ["A", "A", "B"])
print(markovModel)
// or
print(markovModel.chain)

// It will print
   B     A    

| 0.00  0.50 |  B   
|            |
| 0.00  0.50 |  A   
```


# FAQ
> What about the states with zero transitions?

- For memmory safe and performance, they are not even considered by the `MarkovModel`, once they have no effect over the Decision Process.
