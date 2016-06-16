#Data Normalization in OpenRefine

##General Normalization Functions

OpenRefine can help with data that has internal problems. This application is great at fixing those problems while also considering the complete set of values in a dataset. Enhancing data with OpenRefine by bringing information from other sources is also possible and there are many ways to do that, like integrating data from other columns or fetching information from external services.

##Common scenarios

- Identifying unique values accross a dataset
- Identifying how many instances of a value exist in a dataset
- Identifying values that refer to the same concept (people, places, dates, etc.) but that are expressed inconsistently
- Separating values grouped together in a single cell
- Reformatting value structures
- Identifying missing information
- Enhancing data with information available elsewhere in your dataset or from an external resource.


##Sample dataset
For this workshop we will use an adapted version of the [Peel's Prairie Provinces](http://peel.library.ualberta.ca/index.html) metadata. This dataset contains a subset of metadata for the Postcards and Maps collections.

![](../screenshots/postcards.png)
![](../screenshots/maps.png)

Our end goal is to prepare the dataset for visualization in Tableau. To do so we will:

1. normalize and clean up the data
2. reconcile names against an external source
3. geocode a subset of the dataset


## OpenRefine Basics

###Layout
- Presents data in tabular format
- Each row represents a record (or part of it) in the data
- Each column represents a type of information
- Operations are started through column menus

###Exercise 1: Basic Operations
1) Reorder any column and remove another (we will undo this change so don't worry about losing data).

![reorder_column](../screenshots/reorder_column.png)
![reorder_remove](../screenshots/reorder_remove.png)

2) Rename the column "Ocurrence" to "Any Name"

![rename_column](../screenshots/rename_column.png)

3) Undo the previous two actions by going to the *Undo/Redo* panel in the upper left corner, and clicking on the first project state (Create project) or the last action you want to go back to. Changes will be applied automatically.

![undo](../screenshots/undo.png)


4) Sort data based on any of the columns. 

![sort](../screenshots/sort.png)

5) Go back to the *Facet/Filter* panel.

###Exercise #2: Faceting, Clustering, and Cleaning Up Data
1) Facet on the "Path" column

![facet_text](../screenshots/facet_text.png)

2) Facet on the "Content" column as well. If this facet does not display data, click on *Set count choice limit* to increase the number of facets allowed. For this excercise, set it up to 4000.

![facet_two_columns](../screenshots/facet_two_columns.png)

3) Click on two or three "Path" facets and see how the results adapt in the "Content" facet panel.

4) Reset your facets (you can use the *reset* option or hover over a facet and click on *exclude*).

5) Facet again, but this time we want to get all geographical names in the dataset. To do that, facet on the following paths only:

```
/mods/originInfo/place/placeTerm
/mods/subject/geographic
```

6) Check the "Content" data and correct a few values using facets. This option edits all instances of a value in one step. For example, it looks like there a few different values for "Calgary, AB". You can consolidate all values by editing the facets directly. Just click on the edit option, available from each facet:

![facet_calgary](../screenshots/facet_calgary.png)

###Other facets
There are many other ways to facet data
**Numeric and Timeline** facets needs numeric values, so text strings need to be converted to either a number or date format first. This option display graphs and not lists of values.

**Scatterplot facets** display a graphical representation of numerical values for usually two variabes using Cartesian coordinates.

The **word facet** splits strings contained in cells into single words, counts their occurrences throughout the column, and then lists unique words and their occurrence count in the facet panel. This is a way of selecting rows where the contents of a particular column contain one or more specified words. (The user defined GREL custom text facet `split(value," ")` replicates this facet option.

The **duplicates facet** returns boolean values of true and false; filtering on true values returns all the rows that have duplicated values within a particular column; filtering on false displays all unique rows.

The **text length** facet produces a facet based on the character count of strings in cells within the faceted column; the custom numeric facet length(value) achieves something similar; the related measure, word count, can be achieved using the custom numeric facet `length(split(value," "))`.

###Excercise 3: Clustering Facet values
You can also use a number of clustering algorithms built into OpenRefine for seeing what values should probably be the same. 


1) Open your relevant facet, then click on the 'Cluster' button in the top right corner of the Facets box:

![cluster](../screenshots/cluster.png)

You can decide to merge matched values by checking their check box, then clicking on 'Merge Selected and Recluster'. You can change the clustering algorithms in that box as well.

![cluster_actions](../screenshots/cluster_actions.png)


##Transformations
###Excercise #4: Transforming data with GREL and regular expressions

1) Start by executing a replace action. The column "Path" contains full MODS 'routes' for each data field. The root element 'mods' is redundant, so to make the paths a bit easier to read, we can apply a GREL transformation. In this column's menu select **Edit cells > Transform...**

![transform_1](../screenshots/transform_1.png)

Then use the GREL expression `value.replace("/mods/","")`. This expression is asking to replace the string `/mods/` with an empty string. Note that the preview column shows sample results before applying the expression to the complete column.

![transform_2](../screenshots/transform_2.png)

Click OK to apply.


2) In this step we will learn how to add a new column bsaed on an existing column. For the visualization, we need to split the values in the "Path" column into two separate columns. The first should contain the top parent element (e.g. name) and the second the rest of the path value (e.g. namePart).

First make a new column:

![add_column](../screenshots/add_column.png)

Then apply either of the following GREL expressions (same result):

`value.replace(/(.*?)\/(.*)/,"$1")`

or

`value.match(/(.*?)\/.*/)[0]`

The first expression is setting an instruction to take the original value and then *replace* the full string with the first captured group (string before the first `/`), while the second GREL is *matching* the value before the first `/` and dismissing the rest of the data. 

![add_column_parent](../screenshots/add_column_parent.png)

Set the new column name as "parent" and click "OK".

**3) Adapt the previous step to create another column also based on the "Path" column, but this time, we need to copy the second part of the value, i.e. the descendant elements of the parent node**



##[Next: Data Reconciliation](https://github.com/code4libyeg/openrefine_workshop_2016/tree/master/instructions/reconciliation)


##Sources:
http://enipedia.tudelft.nl/wiki/OpenRefine_Tutorial

http://www.meanboyfriend.com/overdue_ideas/wp-content/uploads/2014/11/Introduction-to-OpenRefine-handout-CC-BY.pdf

https://github.com/LODLAM/LODLAMTO16/tree/master/OpenRefine_Tutorial/Instructions/Cleaning