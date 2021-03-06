---
layout: default
title: Data Science and Machine Learning Projects – Summer of Code
---

{% include toc.html %}

## Model Zoo Examples

[Flux](https://github.com/FluxML/Flux.jl)'s [model zoo](https://github.com/FluxML/model-zoo/) contains examples of a wide range of deep learning models and techniques. This project would involve adding new models, showing how to recreate state-of-the-art results (e.g. AlphaGo) or interesting and unusual model architectures (e.g. transformer networks).

Some experience with implementing deep learning models would be ideal for this project, but is not essential for a student willing to pick up the skills and read ML papers.

**Mentors**: [Mike Innes](https://github.com/MikeInnes/)

## Flux.JS demos

[Flux.JS](https://github.com/FluxML/FluxJS.jl) enables export of [Flux](https://github.com/FluxML/Flux.jl) models to the browser. However, just porting a numerical function to JavaScript is rarely exciting on its own; you need to build an interface to give input to the model (say, via a webcam) and see output (say, by displaying an annotated image) in order to see what the model is thinking.

This project would involve creating new demos that show interesting models running in the browser. Examples could include:

* An MNIST digit classify running on hand-drawn images;
* An autoencoder that allows moving sliders to generate images, and explore "digit space";
* A Chess or Go AI that plays against the user;
* A language analysis tool that classifies user-written text.

The possibilities are pretty much endless here. This project will require a pretty solid handle on web technologies, and we'd expect much of the components created to be reusable between demos.

**Mentors**: [Mike Innes](https://github.com/MikeInnes/), [Shashi Gowda](https://github.com/shashi).

## Model Import and Export

Sharing models with other frameworks would enables us to both export models (say to JavaScript for the browser, or TensorFlow Lite for mobile, or NNVM for optimised training) and to take advantage of the large set of [trained models in the wild](https://github.com/BVLC/caffe/wiki/Model-Zoo) in Julia code.

This involves several stages, some or all of which could be tackled over the course of a project.

* Reading and writing the raw model formats. For formats like [ONNX](https://github.com/onnx/onnx) this should be relatively easy, as one can use the [ProtoBuf.jl](https://github.com/JuliaIO/ProtoBuf.jl) library.
* For model import:
  * Converting the raw model format to a more general graph format, such as a [DataFlow.jl](https://github.com/MikeInnes/DataFlow.jl) graph.
  * Dumping the model graph as Julia code.
* For model export:
  * Converting a general graph format to the raw model constructs.
  * Tracing Julia code to produce a dataflow graph, as in [FluxJS.jl](https://github.com/FluxML/FluxJS.jl).

**Mentors**: [Mike Innes](https://github.com/MikeInnes/)

## Benchmarks

A benchmark suite would help us to keep Julia's performance for ML models in shape, as well as revealing opportunities for improvement. Like the model-zoo project, this would involve contributing standard models that exercise common ML use case (images, text etc) and profiles them. The project could extend to include improving performance where possible, or creating a "benchmarking CI" like Julia's own [nanosoldier](https://github.com/JuliaCI/Nanosoldier.jl).

**Mentors**: [Mike Innes](https://github.com/MikeInnes/)

## Compiler Optimisations

Julia opens up many interesting opportunities for applying new optimisations to ML models, and exploring [language design for ML](https://julialang.org/blog/2017/12/ml&pl). As part of this project you'd help us apply novel optimisation strategies to Julia code, with immediate benefits to Flux and other Julia users.

Possible projects could include:

* Auto-parallelisation and vectorisation in the vain of [DyNet autobatch](http://dynet.readthedocs.io/en/latest/tutorials_notebooks/Autobatching.html), [TensorFlow Fold](https://github.com/tensorflow/fold) and [Matchbox](https://github.com/jekbradbury/Minibatch.jl).
* Using [Cassette](https://github.com/jrevels/Cassette.jl/) and techniques similar to [Flux.JS](https://github.com/FluxML/FluxJS.jl) to extract dataflow computation graphs from imperative Julia code.
* Applying optimisations to computation graphs, such as eliding memory allocations, reusing memory and fusing operations, or enabling model parallelism.
* Applying [Halide](http://halide-lang.org/) or [Futhark](https://futhark-lang.org/)-like optimisations to array expressions, as in [Tokamak](https://github.com/MikeInnes/Tokamak)
* Improving Julia's GPU support, including tuning memory management and supporting CUDA streams.

**Mentors**: [Mike Innes](https://github.com/MikeInnes/)

## Sparse GPU and ML support

While Julia supports dense GPU arrays well via [CuArrays](https://github.com/JuliaGPU/CUSPARSE.jl), we lack up-to-date wrappers for sparse operations. This project would involve wrapping CUDA's sparse support, with [CUSPARSE.jl](https://github.com/JuliaGPU/CUSPARSE.jl) as a starting point, adding them to CuArrays.jl, and perhaps demonstrating their use via a sparse machine learning model.

**Mentors**: [Mike Innes](https://github.com/MikeInnes/)

## Making Aquiring Open-Data Easy

Goverments and Universities are releasing huge amounts of data under Open Data policies.
Web portals such as:
 - http://data.gov
 - http://data.gov.au
 - https://dataverse.harvard.edu/
 - http://datadryad.org/
 - https://figshare.com/
 
Expose great quanities of data just wating to be used.

[DataDeps.jl](https://github.com/oxinabox/DataDeps.jl) is a package that helps data scientists ensures that anyone running their code has all the data it needs, no matter when or where it is run.
To do this it needs a registration block, which is a chunk of julia code which says where the data can be download, who created it, what terms and conditions are on its use etc.
For a simple dataset that is all in one file writing this is pretty easy -- copy and paste the info from the website hosting the data.
When you want to dozens of datasets, some of which have dozens of files (and no easy way to download a .zip of all of them), writing this registration block is a bit more work.

[DataDepsGenerators.jl](https://github.com/oxinabox/DataDepsGenerators.jl) exists to solve that.
Give it a URL (or other identifier) for a page describing a dataset, and outputs all the code for a registration block, that you can copy and paste straight into your julia project.
Right now DataDepsGenerators only supports a couple of sites: GitHub (for https://github.com/BuzzFeedNews/ and https://github.com/fivethirtyeight/data/ and others) and the [UCI ML Repository](https://archive.ics.uci.edu/ml/datasets/).
This project aims to change that by adding support for the [CKAN](http://docs.ckan.org/en/latest/api/index.html) and the [OA-PMH](https://www.openarchives.org/OAI/openarchivesprotocol.html) APIs.

The [CKAN](http://docs.ckan.org/en/latest/api/index.html) and the [OA-PMH](https://www.openarchives.org/OAI/openarchivesprotocol.html) APIs allow the automated extraction of metadata for a dataset.
They are primarily used by goverment "data.gov.\*" sites and research repositories respectively.
Together they host millions of datasets, furfilling those institutions open data policies.

This project is to leverage those APIs, to allow others to leaverage those data repositories to produce easily repeatable, data driven research.


**Expected Results**: a series of patches to [DataDepsGenerators.jl](https://github.com/oxinabox/DataDepsGenerators.jl), giving it the capacity to generate a DataDeps registration block for any dataset hosted on site exposing a CRAN, or OAI-PMH API.

**Recommended Skills**: Familarity with web APIs and related technolgies (e.g. REST, JSON, XML (Probably not OAUTH, but if you've done OAUTH then your more than familar enough)). Some practice with webscraping is likely to be useful. A love of data and of doing cool things with it, is a big plus.

**Mentors**: [Lyndon White (oxinabox)](https://github.com/oxinabox/)

## Parameter estimation for nonlinear dynamical models

Machine learning has become a popular tool for understanding data, but scientists
typically understand the world through the lens of physical laws and their
resulting dynamical models. These models are generally differential equations
given by physical first principles, where the constants in the equations such
as chemical reaction rates and planetary masses determine the overall dynamics.
The inverse problem to simulation, known as parameter estimation, is the process
of utilizing data to determine these model parameters.

The purpose of this project is to utilize the growing array of statistical,
optimization, and machine learning tools in the Julia ecosystem to build
library functions that make it easy for scientists to perform this parameter
estimation with the most high-powered and robust methodologies. Possible projects
include investigating methods for Bayesian estimation of parameters via Stan.jl
and Julia-based libraries like Turing.jl, or global optimization-based approaches.
Novel techniques like classifying model outcomes via support vector machines
and deep neural networks is can also be considered. Research and benchmarking
to attempt to find the most robust methods will take place in this project.

Some work in this area can be found in
[DiffEqParamEstim.jl](https://github.com/JuliaDiffEq/DiffEqParamEstim.jl)
and [DiffEqBayes.jl](https://github.com/JuliaDiffEq/DiffEqBayes.jl). Examples
can be found [in the DifferentialEquations.jl documentation](http://docs.juliadiffeq.org/latest/analysis/parameter_estimation.html).

**Recommended Skills**: Background knowledge of standard machine learning,
statistical, or optimization techniques. It's recommended but not required that
one has basic knowledge of differential equations and DifferentialEquations.jl.
Using the differential equation solver to get outputs from parameters can
be learned on the job, but you should already be familiar (but not necessarily
an expert) with the estimation techniques you are looking to employ.

**Expected Results**: Library functions for performing parameter estimation
and inferring properties of differential equation solutions from parameters.
Notebooks containing benchmarks determining the effectiveness of various methods
and classifying when specific approaches are appropriate will be developed
simultaneously.

**Mentors**: [Chris Rackauckas](https://github.com/ChrisRackauckas)

## Artificial Intelligence Library Package based on Artificial Intelligence - A Modern Approach (AIMA)

Often AI and ML are considered synonymous fields, while in most cases the scope 
and focus is entirely different. AI is a field of identification of intelligent 
problems and developing representational frameworks which can aid arriving at a 
solution better. AI establishes or ensures you set up the problem domain properly.
Apply disparate solution schemes using existing technologies based on determistic 
methods or non-deterministic methods to arrive at a solution. The scope of AI is 
establishing the architecture for solution and ML is to actually solve the problem.
Not all problems can be solved by all ML techniques known. For someone to be able 
to try out various schemes to the similar problems may end up rearchitect the 
problem again for new algorithm. Two examples below can provide concrete 
visualization to the claims. 

**Information Extraction** - Using ML to identify text extraction pattern is well
researched problem in the domain. However, many simple structured text can be 
extracted by regular expressions itself. More non-deterministic cases should be 
passed onto a ML based system. However, it's important to model the code in a manner
such that both the solutions can be applied on the same problem abstractions. Text
architectures like GATE provide interesting architectural reprentations for such 
cases. 

**Search Problems** - What is similarity between a traveling sales person problem,
a N-queens placement puzzle and a tic-tac-toe problem? They all seem like graph 
theory problems. You can apply breadth fast, depth fast, A* or many similar classical 
graph search algorithms to it. Can you apply genetic algorithm to solve the problems?
Does that mean you have to completely redesign your problem based on every solution 
framework you have in mind? If you have to solve N-queens by mere recursive search
you have to specifically write code for it in a nifty way. One such implementation is 
in Julia as a sample test code. In AI all these are classified under search problems. 
Solution frameworks are solvers, may it be classic graph theoretic approaches or ML
systems like Genetic Algorithms or Simulated Annealing or even some form of Neural 
Networks. If you have abstractions well defined you could try many of the standard
solvers and use the one which meets your needs best. AI scientists spend enormous 
amount of energy in trying one solution over the the other till they get the best fit.
And a good problem architecture makes that plug-play trial easier. 

**Why AIMA?** - Following are a few reasons I can think of:

1. AIMA is a seminal text on representation of agents that can aid solve a problem for 
an environment of varying complexity. 
2. Contributed by industry and academicians in general has enriched its content over 
past two decades and may of the proposed architectures are vetted time and again. The
book has updated several times and each revision kind of presents itself as a 
significant rewrite with all modern content. 
3. The book is almost read by every AI engineer as a text for their graduation studies.
So most people can connect to the content very easily. 

**Why it's relevant to Julia?** - Here are some of the reasons I can think of
1. Most packages available today as AI packages focus on  the ML solvers as AI. If you 
search the internet on the AI packages you will only get details of ML approaches used 
today. Very few will talk about representational aspects of AI. 
2. Julia with abstracted type systems and multiple dispatch interfaces provide an ideal 
language to represent the problem abstractions best as strategy patterns of software 
engineering. So you can write the AIMA algorithms very easily as method with no side 
effects in generic form. 
3. Julia provides connectivity to other languages for using their libraries. Thus makes
an ideal choice to represent the framework while can use solvers from other languages. 
4. While AIMA authors have developed the sample code, their focus is more towards 
developing sample code for teaching and learning and not professional usage of algorithms.

**Deliverables**

The scope of the project is to create a library of core algorithms and sample programs 
separated out neatly such that core algorithms can be used by practitioners for abstract
problem representation. 

An attempt has been made by me: [AIMACore](https://github.com/sambitdash/AIMACore.jl) and 
[AIMASamples](https://github.com/sambitdash/AIMASamples.jl). `AIMACore` can easily be 
used by a practitioner in their production projects while `AIMASample` can provide examples
or testcases for the `AIMACore`. The current code has tried to address all the search 
problems cases. There is a need to extend it to the rest of AIMA sample code. 

Since, it's an already known problem set it's fairly straight forward in definition. 

**Skillset**

1. A person should be knowledgable in Julia programming or ready to learn it quickly. 
2. Should have appreciation for software engineering principles. A framework requires a 
lot on architectural skills.
3. Ideally, has either undergone a course in AI or wants to invest time in reading and 
applying AIMA. 


