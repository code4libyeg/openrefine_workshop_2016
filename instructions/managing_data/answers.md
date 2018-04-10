##Answer to [Data Normalization Exercise #4](https://github.com/code4libyeg/openrefine_workshop_2016/tree/master/instructions/managing_data#excercise-4-transforming-data-with-grel-and-regular-expressions), step 3:

`value.replace(/(.*?)\/(.*)/,"$2")`

or

`value.match(/.*?\/(.*)/)[0]`

or

`value.partition(/\//)[2]`

