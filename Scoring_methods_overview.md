**Please note: This is NOT a comprehensive listing of all scoring methods that exists.**
Rather, we try to provide an overview of the confidence scoring methods that are known to us. As confidence scoring of interactions is a very diverse field (and many methods that can be used to assess the reliability of an interaction have not originally been developed for this purpose) the list below is not comprehensive. If you know a method that is not included in our list, please contact us or add a reference or a link in the comment to this page.

# Scoring methods #

The order of the following list is completely arbitrary and does not provide information if a method is "better" than another. Instead, we believe that only a mixture of scoring methods can really provide information on the reliability of a particular interactions, as each scoring method is based on different biological aspects.

## MINT score ##
The MINT score takes into account experimental evidence associated with the interaction detection method.

Range: 0-1

Further information: [http://mint.bio.uniroma2.it/mint/doc/MINT-confidence-score.html](http://mint.bio.uniroma2.it/mint/doc/MINT-confidence-score.html)

Reference: [Chatr-aryamontri A et al. MINT: the Molecular INTeraction database. Nucleic Acids Res. 2007 Jan;35(Database issue):D572-4](http://www.ncbi.nlm.nih.gov/pubmed/17135203)

**PSISCORE server: [Listed in the PSISCORE registry](http://psiscore.bioinf.mpi-inf.mpg.de/registry?name=mint)**


## iRefIndex scores ##
[iRefIndex](http://irefindex.uio.no/wiki/iRefIndex) calculates three scores based on the publications that provide evidence for an interaction.

**lpr (lowest pmid re-use)** defines the lowest number of distinct interactions that a publication supporting the interaction is used to support. Low values (e.g. one) indicate that at least one of the publications that support an interaction has only reported few (for one this means no other) interactions, which is likely the case for low-throughput experiments.
Range: 0-inf

**hpr (highest pmid re-use)** is the highest number of interactions that a publication supporting the interaction is used to support. High values indicate that a publication describes many other interactions as well, which is likely the case for high-throughput methods.
Range: 0-inf

**np (number pmids)** is the total number of unique publications used to support the interaction. Higher values indicate that an interaction has been reported in multiple publications.
Range: 0-inf

Further information: [http://irefindex.uio.no/wiki/README\_iRefIndex\_MITAB\_6.0#Column\_number:\_15\_.28confidence.29"](http://irefindex.uio.no/wiki/README_iRefIndex_MITAB_6.0#Column_number:_15_.28confidence.29")

Reference: Razick et al. iRefIndex: A consolidated protein interaction database with provenance http://www.biomedcentral.com/1471-2105/9/405/abstract

**PSISCORE server: [Listed in the PSISCORE registry](http://psiscore.bioinf.mpi-inf.mpg.de/registry?name=irefindex)**

## MI score ##
The MI score is calculated based on the number of publications, the experimental detection methods and the interaction types that support a certain interaction.

Range: 0-1

Further information: [https://docs.google.com/Doc?docid=0AQ\_p-HKWUjHoZGQ5cGNtcmhfMjJ2ZDdwcDhmag&hl=en](https://docs.google.com/Doc?docid=0AQ_p-HKWUjHoZGQ5cGNtcmhfMjJ2ZDdwcDhmag&hl=en)

**PSISCORE server: [Listed in the PSISCORE registry](http://psiscore.bioinf.mpi-inf.mpg.de/registry)**

## Braun et al. ##
Braun et al. propose an experimentally derived confidence score for binary protein interactions.

Reference: [Braun et al. An experimentally derived confidence score for binary protein-protein interactions. Nature Methods 6, 91 - 97 (2008)](http://www.nature.com/nmeth/journal/v6/n1/abs/nmeth.1281.html)