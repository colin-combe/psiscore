# Introduction #
The [PSISCORE Registry](http://psiscore.bioinf.mpi-inf.mpg.de/registry) maintains a list of all available scoring servers and their scoring routines. This allows new service providers to make their resource available to PSISCORE clients simply by including it into Registry. The Registry can be queried in an automatic fashion or it can be browsed via a dedicated website.

The PSISCORE Registry can be found at
**[http://psiscore.bioinf.mpi-inf.mpg.de/registry](http://psiscore.bioinf.mpi-inf.mpg.de/registry)**.

# Accessing the Registry #
If you open the [PSISCORE Registry](http://psiscore.bioinf.mpi-inf.mpg.de/registry) in a web browser you will see a tabular representation of the available scoring servers. You can influence the Registry response through a number of parameters (which have been chosen to correspond to the [PISCQUIC Registry](http://code.google.com/p/psicquic/wiki/Registry) whereever possible).

The full URL of the Registry with all possible parameters can be seen below

```
http://psiscore.bioinf.mpi-inf.mpg.de/registry?action=${ACTION}&format=${FORMAT}&name=${NAME} 
```

## the `action` parameter ##
The `action` parameter defines if you will get a list of all available scoring server or only those that are active/inactive.

|**value**|**description**|**example**| |
|:--------|:--------------|:----------|:|
|STATUS   |list all available PSISCORE servers|http://psiscore.bioinf.mpi-inf.mpg.de/registry?action=STATUS|
|ACTIVE   |list only active PSISCORE servers, i.e., those that are online|http://psiscore.bioinf.mpi-inf.mpg.de/registry?action=ACTIVE|
|INACTIVE |list only inactive PSISCORE servers, i.e., those that cannot currently be contacted by the Registry|http://psiscore.bioinf.mpi-inf.mpg.de/registry?action=INACTIVE|


## the `format` parameter ##
The `format` parameter defines the output format that the Registry uses to present the results.

|**value**|**description**|**example**| |
|:--------|:--------------|:----------|:|
|none     |tabular HTML output|http://psiscore.bioinf.mpi-inf.mpg.de/registry|
|XML      |XML output, containing most of the information shown in the HTML output|http://psiscore.bioinf.mpi-inf.mpg.de/registry?format=XML|
|TXT      |basic text output, containing only server name and SOAP URL|http://psiscore.bioinf.mpi-inf.mpg.de/registry?format=TXT|


## the `name` parameter ##
The `name` parameter can be used to limit the query to a particular scoring server, for instance, to retrieve only its scoring methods. If no scoring server with the name exists, the Registry will not show any results. The name parameter is not case-sensitive.

|**value**|**description**|**example**| |
|:--------|:--------------|:----------|:|
|none     |all scoring servers will be listed|http://psiscore.bioinf.mpi-inf.mpg.de/registry|
|name of a scoring server, e.g., "MINT" or "mint"|only the scoring server with the same name will be listed |http://psiscore.bioinf.mpi-inf.mpg.de/registry?name=MINT|


## Programatically accessing the Registry ##
As described above, you can retrieve a list of scoring servers in different machine readable formats.

#### Plain text ####
If you are only interested in the scoring server and their SOAP adresses, the fastest way is to request a plain text response.

You can use this query to retrieve all active scoring servers:

http://psiscore.bioinf.mpi-inf.mpg.de/registry?action=active&format=txt

The response will look like this:
```
IRefIndex=http://irefindex.uio.no/psiscore-ws/webservices/psiscore
MINT=http://mint.bio.uniroma2.it/psiscore-ws-0.9.7-SNAPSHOT/webservices/psiscore
MI Score=http://www.ebi.ac.uk/enfin-srv/miscore/webservices/psiscore
MPII=http://psiscore.bioinf.mpi-inf.mpg.de/psiscorews/webservices/psiscore
```
Each line describes a PSISCORE server, consisting of a unique ID and the SOAP adress for the server. PSISCORE being a decentralized system, the response to this query will change over time.

#### XML ####
In case you want to retrieve additional information, such as descriptions of the individual scoring methods, you have to use the XML based format. The following query will retrieve the descirption of all scoring methods that the iRefIndex scoring server provides.

http://psiscore.bioinf.mpi-inf.mpg.de/registry.php?name=mi%20score&format=xml


The response will look like this (response is shortened):

```
<registry>
  <service>
  <name>MI Score</name>
  <soapUrl>http://www.ebi.ac.uk/enfin-srv/miscore/webservices/psiscore</soapUrl>
  <active>TRUE</active>
  <version>0.9.7-SNAPSHOT</version>
  <algorithmDescriptor>
    <id>MIscore - intact plus imex curation</id>
    <algorithmType>Replication-based</algorithmType>
    <algorithmType>Method-based</algorithmType>
    <description>A score between 0 and 1 is assigned to each interaction. This score is designed to calculate annotation evidence based on information curated to IMEx or MIMIx standards reporting a molecular interaction experiment. This method will look for annotation evidences coming from all the interaction reported in the IntAct PSICQUIC service and all the IMEX interactions reported by IMEX PSICQUIC services. </description>
    <range>0-1</range>
  </algorithmDescriptor>
  </service>
</registry>
```
Not that there can be multiple `algorithmDescriptor` elements within a `service` element, each representing a different scoring method.

## Adding a new PSISCORE servers ##
The PSISCORE Registry maintained manually. If you want to registry a new service, please send the name and server adress together with a short description of each scoring method that the service provides to hagen (at) mpi-inf.mpg.de. It will be included in the Registry as quick as possible.


## Description of scoring methods ##
PSISCORE servers have to provide a short description in the form of keywords for each scoring method they offer. These keywords should ideally be picked from the [Molecular Interactions controlled vocabulary](http://www.ebi.ac.uk/ontology-lookup/browse.do?ontName=MI). Keywords are intended for automatic classification or selection of certain methods, but they do not provide the user with a comprehensive description of the algorithm details. Therefore, a textual description and optional links to further documentation (for instance, to an external website or a publication) have to be provided as well.