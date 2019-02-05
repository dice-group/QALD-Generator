# QALDGen: Question Answering Over Linked Data Benchmark Generator


QALDGen is Question Answering Over Linked Data (QALD) Benchmarks generation framework which is able to generate customized QALD benchmarks . The framework is flexible enough to generate benchmarks of varying sizes and according to the user-defined criteria on the most important QA features to be considered for Question Answering benchmarking. The generation of benchmarks is achieved by selecting prototypical queries (of a user-defined size and specialized selection criteria) using different clustering algorithms. 
 

 ### Generating Benchmarks from CLI
Download the folder [QALDGen-cli](https://hobbitdata.informatik.uni-leipzig.de/benchmarks-data/QALDGen-cli.zip) which contains a runable jar qaldgen.jar and a comtomized benchmark generation query file personalized-query.txt. Note the qaldgen requires the LSQ dataset endpoint URL to be provided as input. We have provided the Virtuoso 7.2 endpoints both for SWDF and DBpedia datasets which can be downloaded from [here](http://hobbitdata.informatik.uni-leipzig.de/qaldgen-lsq-endpoints/). The Windows virtuoso endpoint can be started from bin/start.bt while linux can be started from bin/start_virtuoso.sh.  
From the folder run the following commands: 
```html
### DBSCAN+Kmeans++ Format ### 
 java -jar qaldgen.jar -m <method> -n <noQuestions> -i <maxNoIterations> -t <noTrialRun> -e <endpointUrl> -q <queryPersonalized> -r <radius> -p <minPts> -o <outputFile>
An example format: 
java -jar qaldgen.jar   -m db+km++   -n 10   -i 10   -t 10   -e http://localhost:8890/sparql   -q personalized-query.txt   -r 1   -p 1   -o db+km++-10qa-benchmark.ttl

### Kmeans++ Format ### 
 java -jar qaldgen.jar -m <method> -n <noQuestions> -i <maxNoIterations> -t <noTrialRun> -e <endpointUrl> -q <queryPersonalized> -o <outputFile>
An example format: 
java -jar qaldgen.jar   -m km++   -n 10   -i 10   -t 10   -e http://localhost:8890/sparql   -q personalized-query.txt   -o km++-10qa-benchmark.ttl


### FEASIBLE Format ### 
 java -jar qaldgen.jar -m <method> -n <noQuestions> -e <endpointUrl> -q <queryPersonalized> -o <outputFile>
An example format: 
java -jar qaldgen.jar   -m feasible   -n 10  -e http://localhost:8890/sparql   -q personalized-query.txt   -o feasible-10qa-benchmark.ttl


### Agglomerative Format ### 
 java -jar qaldgen.jar -m <method> -n <noQuestions> -e <endpointUrl> -q <queryPersonalized> -o <outputFile>
An example format: 
java -jar qaldgen.jar   -m agglomerative   -n 10  -e http://localhost:8890/sparql   -q personalized-query.txt   -o agglomerative-10qa-benchmark.ttl


### FEASIBLE-Exemplars Format ### 
 java -jar qaldgen.jar -m <method> -n <noQuestions> -e <endpointUrl> -q <queryPersonalized> -o <outputFile>
An example format: 
java -jar qaldgen.jar   -m feasible-exmp   -n 10  -e http://localhost:8890/sparql   -q personalized-query.txt   -o feasible-exmp-10qa-benchmark.ttl


### Random Selection Format ### 
 java -jar qaldgen.jar -m <method> -n <noQuestions> -e <endpointUrl> -q <queryPersonalized> -o <outputFile>
An example format: 
java -jar qaldgen.jar   -m random   -n 10  -e http://localhost:8890/sparql   -q personalized-query.txt   -o random-10qa-benchmark.ttl

Where

noQuestions = Number of questions in the benchmark
maxNoIterations = Maximum number of iterations for the KMeans++ clustering algorithm. In our evaluation we used maxNoIterations = 10. 
noTrialRun = Number of trial run for the KMeans++ clustering algorithm. In our evaluation we used noTrialRun = 10.
endpointURL = The endpoint URL hosting the QALD dataset of 5000 questions. The benchmarks are generated from these questions. 
queryPersonalized = The personalized query for costum benchmark generation
radius = Radius for the queries to be considered as outliers. In our evaluation we used radius = 1
minPts = Minimum points or queries in a cluster. In our evaluation we used min. points = 1
outputFile = The output TTL file where the resulting benchmark will be printed

```
### Generating Benchmarks from Source 
Download the source code from [here](https://github.com/AKSW/qaldgen/blob/master/qaldgen-src.7z). Unzip the folder which contains 4 -- Agglomerative, commons-math3, FEASIBLE, qaldgen -- java projects. qaldgen is the main project from where benchmarks can be generated. Note this project requires the other 3 project to be included in the build path. Also all the jar files in the lib folder of FEASIBLE and Agglomerative need to be added into the main project.
```
//Generate KMeans++ benchmarks from 
package org.aksw.simba.sqcbench.centroid
public class KmeansPlusPlus 

//Generate DBSCAN+KMeans++ benchmarks from 
package org.aksw.simba.sqcbench.hybrid
public class DbscanAndKMeansPluPlus 

//Generate FEASIBLE benchmarks from 
package org.aksw.simba.qaldgen.feasible
public class FEASIBLEClustering 

//Generate FEASIBLE-Exemplars benchmarks from 
package org.aksw.simba.qaldgen.feasible
public class FeasibleExemplars

//Generate Random selection benchmarks from 
package org.aksw.simb.sqcbench.random
public class RandomSelection

//You can also generate Agglomerative benchmarks from 
package org.aksw.simba.sqcbench.hierarchical
public class Agglomerative
However, Agglomerative clustering does not allow to generate fix number of clusters
```
### Developers
  * [Muhammad Saleem](https://sites.google.com/site/saleemsweb/) (AKSW, University of Leipzig) 
  * [Kuldeep Singh](https://oyekuldeep.wordpress.com/) (Fraunhofer IAIS, Germany)
  * [Axel-Cyrille Ngonga Ngomo](http://aksw.org/AxelNgonga.html) (AKSW, University of Leipzig)

