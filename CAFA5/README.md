# CAFA 5 Protein Function Prediction
## An Amateur's Journey


The goal of this competition is to predict the function of a set of proteins. Over the next few months I will develop a model trained on the amino-acid sequences of the proteins and on other data. In theory, my work will help researchers better understand the function of proteins, which is important for discovering how cells, tissues, and organs work.

## Steps to come:

- Analysis of the [evaluation metric]
- Exploratory Data Analysis
- Discussion of Cross-Validation Strategy
- A benchmark and a baseline solution
- Feature engineering
- Hyperparameter tuning
- Blending, ensembling and stacking models

## 

The Function Community of Special Interest (Function-COSI) brings together computational biologists, experimental biologists, and biocurators who are dealing with the important problem of gene and gene product function prediction, to share ideas and create collaborations. The Function-COSI holds annual meetings at the Intelligent Systems for Molecular Biology (ISMB) conference and conducts the multi-year Critical Assessment of protein Function Annotation (CAFA) experiment, an ongoing, global, community-driven effort to evaluate and improve the computational annotation of protein function.
As written on the [Competition site]:

> Assigning function to any specific protein can be made difficult due to the multiple functions many proteins have, along with their ability to interact with multiple partners. More knowledge of the functions assigned to proteins—potentially aided by data science—could lead to curing diseases and improving human and animal health and wellness in areas as varied as medicine and agriculture.

> Research groups have developed many ways to determine the function of proteins, including numerous methods based on comparing unsolved sequences with databases of proteins whose functions are known. Other efforts aim to mine the scientific literature associated with some of these proteins, while even more methods combine sophisticated machine-learning algorithms with an understanding of biological processes to decipher what these proteins do. However, there are still many challenges in this field, which are driven by ambiguity, complexity, and data integration.

## [Data]:
The training set includes all proteins with [annotated terms] from the [UniProt]KB release of 2022-11-17 that have been validated by [experimental] or [high-throughput] evidence, traceable author statement (evidence code [TAS]), or inferred by curator ([IC]). (we are not required to train on those data and I'll likely look for more data to supplement with.) The training set lives in five files:

1. Gene Ontology: The [2023-01-01 release of the GO graph] in OBO format. The nodes are indexed by term name
2. Training Sequences: The protein sequences for the training dataset in FASTA format. The header contains metadata such as protein's UniProt accession ID. The sequences are from either the Swiss-Prot database or the TrEMBL database and are all annotated. The header indicates from which database the sequence originates. 
3. Labels: The list of annotated terms, i.e., the ground truth, for the training sequences. Three columns: UniProt accession ID, GO term ID and the [ontology] in which the term appears.
4. Taxonomy: The list of proteins (accession IDs) and the species to which they belong identified by a [taxonomic identifier], or taxon ID, number.
5. Information Accretion: [Information acceration], i.e., weights for each GO term (used to compute precision and recall).

The test superset is a set of protein sequences on which we are asked to predict [GO terms]. It lives in two files:

1. Protein sequences with a UniProt accession ID/taxon ID header
2. A list of all the taxon IDs

The test set will contain protein sequences (and their functions) from the test superset that gained experimental annotations between the submission deadline (August) and the end of the year.





   [Data]: <https://www.kaggle.com/competitions/cafa-5-protein-function-prediction/data>
   [UniProt]: <https://www.uniprot.org/>
   [annotated terms]: <http://geneontology.org/docs/go-annotations/>
   [competition site]: <https://www.kaggle.com/competitions/cafa-5-protein-function-prediction/overview>
   [TAS]: <https://wiki.geneontology.org/index.php/Traceable_Author_Statement_(TAS)>
   [IC]: <https://wiki.geneontology.org/index.php/Inferred_by_Curator_(IC)>
   [experimental]: <https://wiki.geneontology.org/Inferred_from_Experiment_(EXP)>
   [high-throughput]: <https://wiki.geneontology.org/Inferred_from_High_Throughput_Experiment_(HTP)>
   [GO terms]: <http://geneontology.org/docs/GO-term-elements>
   [2023-01-01 release of the GO graph]: <https://data.bioontology.org/ontologies/GO/submissions/1811/download?apikey=8b5b7825-538d-40e0-9e9e-5ab9274a9aeb>
   [taxonomic identifier]: <https://www.uniprot.org/help/taxonomic_identifier>
   [Information acceration]: <https://github.com/claradepaolis/InformationAccretion>
   [ontology]: <http://geneontology.org/docs/ontology-documentation/>

   [evaluation metric]: <https://github.com/bschulman/Data-Science-Portfolio/blob/main/CAFA5/Eval%20Metric.md>
   [PlGh]: <https://github.com/joemccann/dillinger/tree/master/plugins/github/README.md>
   [PlGd]: <https://github.com/joemccann/dillinger/tree/master/plugins/googledrive/README.md>
   [PlOd]: <https://github.com/joemccann/dillinger/tree/master/plugins/onedrive/README.md>
   [PlMe]: <https://github.com/joemccann/dillinger/tree/master/plugins/medium/README.md>
   [PlGa]: <https://github.com/RahulHP/dillinger/blob/master/plugins/googleanalytics/README.md>

