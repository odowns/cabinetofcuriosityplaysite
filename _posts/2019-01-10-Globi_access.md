---
layout: post
title: "Yikang Test"
date: 2018-10-10
author: Ciera Martinez
description: Welcome to a new blog that explores natural history data.
img: workflow.jpg
---

# How to access Globi database :

### Author: Yikang Li  
### Date: Nov, 17th, 2018

## What is GloBi:

Global Biotic Interactions (GloBI) provides open access to species interaction data (e.g., predator-prey, pollinator-plant, pathogen-host, parasite-host) by combining existing open datasets using open source software. By providing an infrastructure to capture and share interaction data, individual biologists can focus on gathering new interaction data and analyzing existing datasets without having to spend resources on (re-) building a cyberinfrastructure to do so.

GloBI is made possible by a community of software engineers, bioinformaticists and biologists. Software engineers such as Jorrit Poelen, Göran Bodtitleenschatz, and Robert Reiz collaborate with bioinformaticists like Chris Mungall, data managers like Sarah E. Miller and biologists like Jim Simons, Anne Thessen, Jen Hammock and Brian Hayden to capture, provide access to and use interaction data that is provided by biologists and citizen scientists around the world. GloBI is funded by EOL's Rubenstein Fellowship Program.


### How to access GloBi:

There is a package called "rglobi" in R which allows us to access the database on Global Biotic Interactions (GloBI).  
  
Description from the documentation of package:  
"A programmatic interface to the web service methods provided by Global Biotic Interactions (GloBI). GloBI provides access to spatial-temporal species interaction records from sources all over the world. rglobi provides methods to search species interactions by location, interaction type, and taxonomic name. In addition, it supports Cypher, a graph query language, to allow for executing custom queries on the GloBI aggregate species interaction data set."  

To use its methods and functions, we need to install and library the package "rglobi" in R.

```r
install.packages("rglobi")
library(rglobi)
```
Users are able to search data on species interactions by location, interaction type, and taxonomic names and so on. 


###### While the r package provides built in methods and functions, it has limitation on the maximum amount of data displayed.
###### To access all the data, getting one of the archives:

#### Choice 1:
Use Pagination: https://github.com/ropensci/rglobi/blob/master/vignettes/rglobi_vignette.Rmd#L410

"By default, the amount of results are limited. If you'd like to retrieve all results, you can used pagination. For instance, to retrieve parasitic interactions using pagination, you can use:


```r
otherkeys = list("limit"=10, "skip"=0)
first_page_of_ten <- get_interactions_by_type(interactiontype = c("hasParasite"), otherkeys = otherkeys)
otherkeys = list("limit"=10, "skip"=10)
second_page_of_ten <- get_interactions_by_type(interactiontype = c("hasParasite"), otherkeys = otherkeys)
```

To exhaust all available interactions, you can keep paging results until the size of the page is less than the limit (e.g., ```nrows(interactions) < limit```)."


#### Choice 2:  
Through API: https://github.com/jhpoelen/eol-globi-data/wiki/API  
The link above contains API which provide access to interaction data for the purpose of integrating the data into wikis, custom webpages or other interaction exploration tools.

#### Choice 3:
Download the whole dataset directly at https://www.globalbioticinteractions.org/data  
Datasets are available to download in different formats including tsv, csv and N-Quads/RDF.

### Import data into Jupyter notebook:


```python
import pandas as pd
```


```python
data =pd.read_csv('./with_new_csv/interactions.tsv', delimiter='\t', encoding='utf-8')
```

    /Users/glance/anaconda3/lib/python3.6/site-packages/IPython/core/interactiveshell.py:3020: DtypeWarning: Columns (13,14,15,16,17,18,19,21,22,23,24,25,26,27,28,29,30,41,42,43,44,45,46,47,48,49,50,55,58,59,60,61,62,63,64,65,68,69,71,72,77) have mixed types. Specify dtype option on import or set low_memory=False.
      interactivity=interactivity, compiler=compiler, result=result)



```python
data.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>sourceTaxonId</th>
      <th>sourceTaxonIds</th>
      <th>sourceTaxonName</th>
      <th>sourceTaxonRank</th>
      <th>sourceTaxonPathNames</th>
      <th>sourceTaxonPathIds</th>
      <th>sourceTaxonPathRankNames</th>
      <th>sourceTaxonSpeciesName</th>
      <th>sourceTaxonSpeciesId</th>
      <th>sourceTaxonGenusName</th>
      <th>...</th>
      <th>localityName</th>
      <th>eventDateUnixEpoch</th>
      <th>referenceCitation</th>
      <th>referenceDoi</th>
      <th>referenceUrl</th>
      <th>sourceCitation</th>
      <th>sourceNamespace</th>
      <th>sourceArchiveURI</th>
      <th>sourceDOI</th>
      <th>sourceLastSeenAtUnixEpoch</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>EOL:4472733</td>
      <td>EOL:4472733 | EOL:4472733</td>
      <td>Deinosuchus</td>
      <td>genus</td>
      <td>Deinosuchus</td>
      <td>EOL:4472733</td>
      <td>genus</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Deinosuchus</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Rivera-Sylva H.E., E. Frey and J.R. Guzmán-Gui...</td>
      <td>10.4267/2042/28152</td>
      <td>NaN</td>
      <td>Katja Schulz. 2015. Information about dinosaur...</td>
      <td>KatjaSchulz/dinosaur-biotic-interactions</td>
      <td>https://github.com/KatjaSchulz/dinosaur-biotic...</td>
      <td>NaN</td>
      <td>2018-11-14T23:55:44.895Z</td>
    </tr>
    <tr>
      <th>1</th>
      <td>EOL:4433651</td>
      <td>EOL:4433651 | EOL:4433651</td>
      <td>Daspletosaurus</td>
      <td>genus</td>
      <td>Daspletosaurus</td>
      <td>EOL:4433651</td>
      <td>genus</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Daspletosaurus</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>doi:10.1666/0022-3360(2001)075&lt;0401:GCFACT&gt;2.0...</td>
      <td>10.1666/0022-3360(2001)075&lt;0401:GCFACT&gt;2.0.CO;2</td>
      <td>NaN</td>
      <td>Katja Schulz. 2015. Information about dinosaur...</td>
      <td>KatjaSchulz/dinosaur-biotic-interactions</td>
      <td>https://github.com/KatjaSchulz/dinosaur-biotic...</td>
      <td>NaN</td>
      <td>2018-11-14T23:55:44.895Z</td>
    </tr>
    <tr>
      <th>2</th>
      <td>EOL:24210058</td>
      <td>EOL:24210058 | OTT:3617018 | GBIF:4975216 | EO...</td>
      <td>Repenomamus robustus</td>
      <td>species</td>
      <td>Eucarya | Opisthokonta | Metazoa | Eumetazoa |...</td>
      <td>EOL:5610326 | EOL:2910700 | EOL:42196910 | EOL...</td>
      <td>|  | subkingdom |  |  |  |  |  |  |  |  | supe...</td>
      <td>Repenomamus robustus</td>
      <td>EOL:24210058</td>
      <td>Repenomamus</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>doi:10.1038/nature03102</td>
      <td>10.1038/nature03102</td>
      <td>NaN</td>
      <td>Katja Schulz. 2015. Information about dinosaur...</td>
      <td>KatjaSchulz/dinosaur-biotic-interactions</td>
      <td>https://github.com/KatjaSchulz/dinosaur-biotic...</td>
      <td>NaN</td>
      <td>2018-11-14T23:55:44.895Z</td>
    </tr>
    <tr>
      <th>3</th>
      <td>EOL:4433892</td>
      <td>EOL:4433892 | EOL:4433892</td>
      <td>Sinocalliopteryx gigas</td>
      <td>species</td>
      <td>Sinocalliopteryx gigas</td>
      <td>EOL:4433892</td>
      <td>species</td>
      <td>Sinocalliopteryx gigas</td>
      <td>EOL:4433892</td>
      <td>NaN</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>doi:10.1371/journal.pone.0044012</td>
      <td>10.1371/journal.pone.0044012</td>
      <td>NaN</td>
      <td>Katja Schulz. 2015. Information about dinosaur...</td>
      <td>KatjaSchulz/dinosaur-biotic-interactions</td>
      <td>https://github.com/KatjaSchulz/dinosaur-biotic...</td>
      <td>NaN</td>
      <td>2018-11-14T23:55:44.895Z</td>
    </tr>
    <tr>
      <th>4</th>
      <td>EOL:4433892</td>
      <td>EOL:4433892 | EOL:4433892</td>
      <td>Sinocalliopteryx gigas</td>
      <td>species</td>
      <td>Sinocalliopteryx gigas</td>
      <td>EOL:4433892</td>
      <td>species</td>
      <td>Sinocalliopteryx gigas</td>
      <td>EOL:4433892</td>
      <td>NaN</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>doi:10.1371/journal.pone.0044012</td>
      <td>10.1371/journal.pone.0044012</td>
      <td>NaN</td>
      <td>Katja Schulz. 2015. Information about dinosaur...</td>
      <td>KatjaSchulz/dinosaur-biotic-interactions</td>
      <td>https://github.com/KatjaSchulz/dinosaur-biotic...</td>
      <td>NaN</td>
      <td>2018-11-14T23:55:44.895Z</td>
    </tr>
  </tbody>
</table>
<p>5 rows × 79 columns</p>
</div>



### Basic data exploration and characteristics:


```python
#check the number of rows:
len(data)
```




    3445494



#### Columns in the database:  


```python
data.columns
```




    Index(['sourceTaxonId', 'sourceTaxonIds', 'sourceTaxonName', 'sourceTaxonRank',
           'sourceTaxonPathNames', 'sourceTaxonPathIds',
           'sourceTaxonPathRankNames', 'sourceTaxonSpeciesName',
           'sourceTaxonSpeciesId', 'sourceTaxonGenusName', 'sourceTaxonGenusId',
           'sourceTaxonFamilyName', 'sourceTaxonFamilyId', 'sourceTaxonOrderName',
           'sourceTaxonOrderId', 'sourceTaxonClassName', 'sourceTaxonClassId',
           'sourceTaxonPhylumName', 'sourceTaxonPhylumId',
           'sourceTaxonKingdomName', 'sourceTaxonKingdomId', 'sourceId',
           'sourceOccurrenceId', 'sourceCatalogNumber', 'sourceBasisOfRecordId',
           'sourceBasisOfRecordName', 'sourceLifeStageId', 'sourceLifeStageName',
           'sourceBodyPartId', 'sourceBodyPartName', 'sourcePhysiologicalStateId',
           'sourcePhysiologicalStateName', 'interactionTypeName',
           'interactionTypeId', 'targetTaxonId', 'targetTaxonIds',
           'targetTaxonName', 'targetTaxonRank', 'targetTaxonPathNames',
           'targetTaxonPathIds', 'targetTaxonPathRankNames',
           'targetTaxonSpeciesName', 'targetTaxonSpeciesId',
           'targetTaxonGenusName', 'targetTaxonGenusId', 'targetTaxonFamilyName',
           'targetTaxonFamilyId', 'targetTaxonOrderName', 'targetTaxonOrderId',
           'targetTaxonClassName', 'targetTaxonClassId', 'targetTaxonPhylumName',
           'targetTaxonPhylumId', 'targetTaxonKingdomName', 'targetTaxonKingdomId',
           'targetId', 'targetOccurrenceId', 'targetCatalogNumber',
           'targetBasisOfRecordId', 'targetBasisOfRecordName', 'targetLifeStageId',
           'targetLifeStageName', 'targetBodyPartId', 'targetBodyPartName',
           'targetPhysiologicalStateId', 'targetPhysiologicalStateName',
           'decimalLatitude', 'decimalLongitude', 'localityId', 'localityName',
           'eventDateUnixEpoch', 'referenceCitation', 'referenceDoi',
           'referenceUrl', 'sourceCitation', 'sourceNamespace', 'sourceArchiveURI',
           'sourceDOI', 'sourceLastSeenAtUnixEpoch'],
          dtype='object')



#### How many different types of taxons as sources & target? 


```python
#source taxon
len(data['sourceTaxonId'].unique())
```




    147156




```python
#Target taxon
len(data['targetTaxonId'].unique())
```




    105196



#### What interaction types are there?


```python
data['interactionTypeName'].unique()
```




    array(['eats', 'preysOn', 'interactsWith', 'pollinates', 'parasiteOf',
           'pathogenOf', 'visitsFlowersOf', 'adjacentTo', 'dispersalVectorOf',
           'hasHost', 'endoparasitoidOf', 'symbiontOf', 'endoparasiteOf',
           'hasVector', 'ectoParasiteOf', 'vectorOf', 'livesOn', 'livesNear',
           'parasitoidOf', 'guestOf', 'livesInsideOf', 'farms',
           'ectoParasitoid', 'inhabits', 'kills', 'hasDispersalVector',
           'livesUnder', 'kleptoparasiteOf', 'hostOf', 'visits', 'eatenBy',
           'flowersVisitedBy', 'preyedUponBy', 'hasParasite', 'pollinatedBy',
           'hasPathogen'], dtype=object)




```python
#number of different types of interaction
len(data['interactionTypeName'].unique())
```




    36



#### Drop duplicates:


```python
data.drop_duplicates(['sourceTaxonId', 'interactionTypeName', 'targetTaxonId'], inplace = True)
```


```python
len(data)
```




    956380


