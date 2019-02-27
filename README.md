# HitPredict
HitPredict is a resource of experimentally identified physical protein-protein interactions that are scored for reliability. 

Data:
1. All physical interactions were downloaded from IntAct, BioGRID, HPRD, DIP and MINT. These are combined to form a non-redundant dataset. Species with less than 10 interactions are removed.
2. All non-physical interactions, such as genetic interactions, are excluded.
3. Interactions of proteins from different species are also excluded.
4. All proteins are assigned valid UniProt IDs. In cases where UniProt IDs cannot be directly assigned, protein sequences are aligned to UniProtKB using BLAST and the ID of the longest hit with 99% sequence identity is used.
5. Interactions in which one or both of the proteins are no longer present in UniProt, are removed.
6. Interactions of proteins that do not map to valid UniProt IDs areremoved. Interactions are excluded only after manual confirmation.
7. The interacting proteins are annotated with Entrez gene IDs, Ensembl IDs, Pfam domains and Gene Ontology terms.

Scoring:
All interactions in HitPredict (small-scale or high-throughput) are assigned an Interaction score. The interaction score denotes the reliability of the interaction and is the geometric mean of the following two methods:

A) Annotation-based Score
This score is calculated in the form of a likelihood ratio using naive Bayesian networks and is based on the following properties of the interacting proteins:
1. Structurally known interacting Pfam domains obtained - 3DID
2. Gene Ontology (GO) annotations of the interacting proteins - GO
3. Homologous interactions - HINTdb
4. Likelihood ratio greater than 1 is scaled to give an annotation score between 0.5 and 1. An annotation score >= 0.5 indicates a high confidence interaction. The value of the annotation score increases with the evidence supporting the interaction. More details about this score can be found here.

B) Method-based Score
This score is based on the experimental information available for the interactions and is calculated as the mean of the following three scores:
1. Publication score: Score based on the number of unique publications or experiments supporting the interaction
2. Method score: Score based on the following methods of interaction identification - biophysical, protein complementation assay, post transcriptional inference, biochemical, imaging technique and their subtypes. The default scores for each method are used as specified by the HUPO PSI-MI consortium.
3. Type score: Score based on the following interaction types and their subtypes - association, physical association and direct interaction. The default scores for each type are used as specified by the HUPO PSI-MI consortium.

These scores are calculated and combined into a single score using the method shown in Villaveces et al., Database, 2015. A method score >= 0.485 is considered to indicate high confidence. This cut-off is suggested by Villaveces et al.

C) Combined Interaction Score
This score is the geometric mean of the Annotation-based score and the Method-based score. As such, it takes into account the experimental support for the interaction as well as the genomic features of the interacting proteins. This score has been shown to have a better performance than either of the two scores as well as the score used by the Mentha database (same as that used by MINT). The ROC curve for this evaluation can be seen here

References:
1. Yosvany Lopez, Kenta Nakai and Ashwini Patil; HitPredict version 4 - comprehensive reliability scoring of physical protein-protein interactions from more than 100 species, Database 2015:bav117, 2015.
2. Ashwini Patil, Kenta Nakai and Haruki Nakamura; HitPredict: a database of quality-assessed protein-protein interactions in nine species, Nucl. Acids Res. 2011 Database Issue:D744-9.
3. Ashwini Patil and Haruki Nakamura; Filtering high-throughput protein-protein interaction data using a combination of genomic features, BMC Bioinformatics, 2005, 6:100.
