# CAFA 5 Protein Function Prediction
## Evaluation Metric


1. Proteins in the test superset that receive new annotations in any of the three subontologies between the competition end and the year-end will be evaluated.
- There are three separate test sets, one for each subontology.
- These test sets may have overlapping proteins.
2. The maximum F-measure, which considers both precision and recall, will be calculated for each subontology's test set.
- Precision and recall measure the accuracy and completeness of predictions.
- The F-measure combines these two metrics to provide an overall evaluation.
3. Each entry will be assessed based on the average of the maximum F-measure from the three subontology test sets.
- This means the performance is evaluated based on the average of the best F-measure from each test set.
4. The goal is to generate predicted ontological annotations in the form of a directed acyclic graph (DAG).
- The predictions represent the possible functions of a protein, interconnected by relationships like "is a," "part of," "has part," "regulates," etc.
- Predictions are a smaller subset of the larger GO graph.
5. It is challenging to accurately predict the complete subgraph of a protein's true functions in the GO graph.
- The true subgraph may not even be fully known.
- The algorithm's objective is to output the best consistent subgraph for each protein, along with confidence levels for both the entire subgraph and individual predicted functions.
6. The evaluation metric used is a graph-similarity metric.
- This metric measures how similar the predicted subgraph is to the actual subgraph.
- It assesses the overall match between the predicted and true functions in a graph-based manner.

Ontologies are used in biomedical sciences to organize and exchange knowledge. They are like graphs where concepts are represented as vertices and relationships as edges. The ontology we use here is the Gene Ontology (GO), which describes gene functions.

To evaluate prediction tools, we need to compare their predicted graphs with the true experimental annotations. The structure of the ontology and the incomplete nature of the annotations make evaluation challenging. Different computational models produce different outputs, so we need to consider that as well.

Developing evaluation metrics is important. We need metrics that measure similarity between predicted and experimental annotations, considering the dependency between terms. These metrics should not only assess correct predictions but also capture mispredictions. Additionally, the metrics should be easy to understand and interpret probabilistically.

When evaluating the performance of prediction tools, we need to measure the similarity between graphs or sets of annotations. Proteins have annotations represented as graphs with nodes (terms) connected by edges (relationships). There are two main categories of metrics: topological and probabilistic.

Topological metrics use the structure of the ontology and compare sets of nodes and edges. Examples include Jaccard and cosine similarity coefficients, as well as precision/recall and ROC curves. These metrics assess overlap between true and predicted terms but may not consider node dependency or unequal specificity of annotations.

Probabilistic metrics assume a probabilistic model over the ontology and use a protein database to learn the model. They measure the information content of shared terms in the ontology and can consider individual annotations. However, they may only provide a single statistic and overlook the tradeoff between precision and recall in predictions.

There are challenges in both types of metrics. Topological measures can be biased and affected by ontology updates, while probabilistic measures may lack justification and struggle with annotations containing multiple leaf terms. Certain semantic similarity metrics assume similar numbers of leaf terms, leading to issues with different prediction algorithms.

Overall, evaluation metrics aim to capture the similarity between predicted and true annotations while considering the complexities of the ontology structure and annotation characteristics.
### Information Content/Accretion

#### Information content of a graph:

Let's consider each term in the ontology as a yes-or-no question, and we don't know the exact probabilities for the answers. We want to evaluate how well a prediction process works, based on the quality of its predictions.

We assume that the relationships between the terms in the ontology can be represented by a network, where each term is connected to its parents. This means that the probability of one term being true or false is independent of the other terms, given its parents. We can break down the overall probability into smaller parts based on these relationships.

What we're interested in is the likelihood that a protein is associated with a specific group of terms in the ontology, based on experimental evidence.

The information content of a subgraph is the number of bits of information one would recieve about a protein if it were annotated with some subgraph $T$: $$i(T)=\log_2{\frac{1}{Pr(T)}}$$
where $Pr(T)=\prod_{\nu\in T}Pr(\nu|Pa(\nu))$ and $Pa(\nu)$ is the set of parent nodes of $\nu$
#### Information content of a node
Then the [Information accretion] for each node in the subgraph measures how much information is added to an ontology annotation by some node $\nu$ given that its parents are already annotated, i.e., the increase, or accretion, of information obtained by adding a child term to a parent term, or set of parent terms, in an annotation.

The weight for each term is [computed] as follows: Each term, $f$, in the ontology is weighted according to its information content: $$ic(f)=\log_2{\frac{1}{Pr(f|\mathbb{P})}}$$ where $Pr(f|\mathbb{P})$ is the conditional probability that $f$ is associated to a given protein given all the terms parents are associated (calculated from the union of SwissProt, UniProt-GOA and GO consortium databases), or the rarity of observing the association between the term and the protein, given the presence of its parent terms and is expressed in units of bits. 
#### Comparing two graphs
Let's imagine a scenario where we have two graphs: one represents the actual function of a protein (let's call it T), and the other represents the predicted function (let's call it P).

Now, we want to measure how well the predicted function matches the actual function. To do this, we define two metrics that are similar to the concepts of recall and precision. We call these metrics remaining uncertainty and misinformation.

Remaining uncertainty refers to the information that is still unknown about the protein's true function, which is not captured by the predicted function graph P. It represents what we still don't know about the protein's function.

Misinformation, on the other hand, measures the total amount of incorrect information introduced by the classifier. It focuses on the nodes along paths in the predicted function graph P that are not correct, adding up the incorrect information.

Using this framework, we can assess how similar the predicted function is to the actual function of the protein. We don't rely on finding a common ancestor between pairs of leaves (which is often referred to as the maximum informative common ancestor), but rather look at the remaining uncertainty and misinformation to evaluate the match.

#### Measuring the quality of a function prediction
In simple terms, when a protein function predictor gives its results, it usually provides scores that indicate how strong or likely the predictions are for each function in a list. To better understand and handle these scores, we need to consider two important things: remaining uncertainty and misinformation.

If a prediction score is equal to or higher than some decision threshold, we consider it a positive prediction, meaning we believe that the protein has that particular function. Anything below the threshold is considered a negative prediction.

Regardless of the specific threshold chosen, each decision threshold gives us a separate pair of values for remaining uncertainty and misinformation. Think of it as different combinations of how sure we are about the protein's function and how much incorrect information is introduced.

To calculate the remaining uncertainty and misinformation for a protein that we have never seen before, we average over a set of known proteins that were used to evaluate the predictor. We consider the entire set of terms that have scores greater than or equal to the threshold, and we create a unique list of the ancestors for those predicted terms.

As we move the decision threshold from its minimum value to its maximum, we create a curve in a two-dimensional space that shows how the pairs of remaining uncertainty and misinformation change. By removing a normalizing constant, we can obtain the total remaining uncertainty and misinformation associated with a database of proteins and a set of predictions.
##### Weighted metrics
We give each protein a weight based on how much useful information its experimental annotation provides. This means that proteins with less informative annotations are given lower weights, while proteins with rare and surprising annotations are given higher weights.

In biological datasets, annotations that are seen frequently tend to be less detailed or shallow. This happens because some experimental techniques have limitations or are designed to handle large amounts of data quickly. As a result, we need to be cautious when relying solely on frequently seen annotations, as they may not give us the full picture of a protein's function.

#### Precision and recall
Weighted precision and recall are calculated as:

$$pr_w(T,P(\tau))=\frac{\sum_{\nu\in T\cap P(\tau)}ia(\nu)}{\sum_{\nu\in P(\tau)}ia(\nu)}$$

$$rc_w(T,P(\tau))=\frac{\sum_{\nu\in T\cap P(\tau)}ia(\nu)}{\sum_{\nu\in P(\tau))}ia(\nu)}$$

where $P(\tau)$ is the set of predicted terms with score $\geq$ the decision threshold $\tau$, and $T$ is the set of the proteins already annotated terms. 

Finally,  $$F_{max}=\max_{\tau}{2\cdot\frac{2pr_w(\tau)\cdot rc_w(\tau)}{pr_w(\tau)+rc_w(\tau)}}$$

### Full Evaluation:
In full evaluation, $ic(f)$ for each $f$ are provided a priori. However, the probabilities they are calculated from are unknown and estimated using the observed annotations in the datasets as the empirical distribution. 







   [Data]: <https://www.kaggle.com/competitions/cafa-5-protein-function-prediction/data>
   [UniProt]: <https://www.uniprot.org/>
   [annotated terms]: <http://geneontology.org/docs/go-annotations/>
   [competition site]: <https://www.kaggle.com/competitions/cafa-5-protein-function-prediction/overview>
   [TAS]: <https://wiki.geneontology.org/index.php/Traceable_Author_Statement_(TAS)>
   [IC]: <https://wiki.geneontology.org/index.php/Inferred_by_Curator_(IC)>
   [experimental]: <https://wiki.geneontology.org/Inferred_from_Experiment_(EXP)>
   [high-throughput]: <https://wiki.geneontology.org/Inferred_from_High_Throughput_Experiment_(HTP)>
   [GO terms]: <http://geneontology.org/docs/GO-term-elements>
   [computed]: <https://ndownloader.figstatic.com/files/7128245>
   [Information accretion]: <https://www.kaggle.com/competitions/cafa-5-protein-function-prediction/discussion/405237>
