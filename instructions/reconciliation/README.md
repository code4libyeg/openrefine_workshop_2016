#Data Reconciliation with OpenRefine

There are many ways to work on data reconciliation with OpenRefine:

- Built-in tools are available from the **Reconciliation** submenu. It is also possible to reconcile fetching information from remote resources via the **Add column by fetching URLs** tool.
- There are around 8 plugins that extend the reconciliation functionality. Some are available from the [OpenRefine download page](http://openrefine.org/download.html).
- OpenRefine integrates with [around 16 reconciliation services](https://github.com/OpenRefine/OpenRefine/wiki/Reconcilable-Data-Sources).


##Dataset
Import the [Peel Author Names and Pseudonyms OpenRefine project] available from []().
This dataset contains author names and biographical information from the Peel Monographs


##Reconciling author names using Open Refine and VIAF
For this exercise we will call a service that can be used to reconcile author names. It uses the Virtual International Authority File (VIAF) API. Using this service we can match authors to VIAF identifiers, widely used in Wikipedia pages and many libraries.




Get rid of words (3> letters)
value.replace(/[a-zA-Z]{3,}/,"")
Split into columns
(\s?-\s?c?\.?\s?)|([fb]l?\.\s?)

Bring death years
 cells["dates 1"].value.replace(/d\.(\d{4})\??\.?/,"$1")

 Some manual cleanup in date 1
 Transformation to delete trailing period in date 3

 Renamed columns

Add the service:
http://iphylo.org/~rpage/phyloinformatics/services/reconciliation_viaf.php
It might take a while to connect to the service.
In the reconcile window you will see options to use data from other columns and to map those columns to specific ontology types. As you type you will see suggestions based on your input that display infoboxes for suggested ontology classes or subclasses. For this excercise, select the following options and classs:
- Reconcile against type: Author

It should take around 3 - 4 minutes to complete.


Sometimes there may be more than one possible match, in which case these will be listed in the cell. Once you have reconciled the data you may want to do something with the reconciliation.

In the box labelled Expression enter cell.recon.match.id and give the column a name 
