# Tutorial: Zika

## SETUP
#### Pre-requisites

**Used Software** -> [Content Mine Virtual Machine (05/2016)](https://drive.google.com/open?id=0B7pJKedx9b97LTBVRmEzbzJOVlU) which consists of: 
- [getpapers](https://github.com/ContentMine/getpapers) (0.4.5), [norma](https://github.com/ContentMine/norma) (0.2.26) and [ami](https://github.com/ContentMine/ami) (0.2.24)
- [Python3](https://www.python.org/) (3.2.3) and [IPython](http://ipython.org/) (4.1.1).
- [pyCProject](https://github.com/ContentMine/pyCProject) (v.)

**Preparation**
- [Install the Virtual Machine](https://github.com/ContentMine/workshop-resources/tree/master/software-tutorials/vms) with the [Virtual Machine Image May 2016](https://drive.google.com/open?id=0B7pJKedx9b97LTBVRmEzbzJOVlU).
- Run through the tutorials of [getpapers](https://github.com/ContentMine/workshop-resources/tree/master/software-tutorials/cproject), [norma](https://github.com/ContentMine/workshop-resources/tree/master/software-tutorials/norma) and [ami](https://github.com/ContentMine/workshop-resources/tree/master/software-tutorials/ami).
- get a basic understanding of what a [CProject](https://github.com/ContentMine/workshop-resources/tree/master/software-tutorials/cproject) and [Scholarly HTML](https://github.com/ContentMine/workshop-resources/tree/master/software-tutorials/sHTML) is.

**Install**
Install pyCProject via pip. Sudo password is ```password```.

```
sudo pip install --upgrade numpy
sudo pip install pycproject
```

## TUTORIALS

#### Download all Zika publications available
The first step always is to get the needed data from the API's. For this we use [getpapers](https://github.com/ContentMine/workshop-resources/tree/master/software-tutorials/cproject), the ContentMine tool for getting papers via different Publisher-API's.

First we want to have a look, how many results we find for the search term "zika".

```bash
getpapers 'zika' -o zika
```
1126 papers are found in our case (14. 03. 2017).

To download then all available PDF's of the found scientific papers, we add an output folder via ```-o zika``` and add ```-p``` to tell that we want PDF's.

```bash
getpapers 'zika' -o zika -p
```

After the download, we want to have a look on the downloaded files in a tree-like directory view.

```bash
tree zika
```

For some of the found publications there is also an XML-file available. To download them, we have to add ```-x``` as a flag to the query. The results then can be viewed again with the tree command.

```bash
getpapers 'zika' -o zika -x
tree zika
```
The query finds 100 XML-files, and can download 98 of them (14. 03. 2017).

Finally to complete our dataset, we also download all supplementary materials available for the zika-publications. Simply add ```-s``` to the query, and view the results as usual.

```bash
getpapers 'zika' -o zika -s
tree zika
```
Of the 100 XML-files for 57 of them supplementary materials can be found, and all have been downloaded.

Now we have all the available data, which can be used for further analysis.

#### Normalize the data

Before we can start with the extraction and analysis, we have to normalize the raw data and convert it to [Scholarly HTML](https://github.com/ContentMine/workshop-resources/tree/master/software-tutorials/sHTML).

For this, we convert the fulltext.xml files to scholarly.html files with [norma](https://github.com/ContentMine/workshop-resources/tree/master/software-tutorials/norma) and view the results.

```bash
norma --project zika -i fulltext.xml -o scholarly.html --transform nlm2html
tree zika
```

#### Extract the needed facts

The prepared data now can be used to extract the facts via [ami](https://github.com/ContentMine/workshop-resources/tree/master/software-tutorials/ami)'s different plugins.

First we use the species plugin to get the genus and binomial nomenclature.

```bash
ami2-species --project zika -i scholarly.html --sp.species --sp.type genus
ami2-species --project zika -i scholarly.html --sp.species --sp.type binomial
ami2-species --project zika -i scholarly.html --sp.species --sp.type genussp
tree zika
```

Second we use the word plugin to get frequencies of words inside a publication. 

```bash
ami2-word --project zika -i scholarly.html --w.words wordFrequencies
```

#### Check word frequencies


#### Check co-occurences of entities

#### Follow Up's

- Do another tutorial from the FutureTDM project 
- Learn more about the tools used with our [software tutorials](https://github.com/ContentMine/workshop-resources)
- [Contribute to this repository](../README.md#contribution)
- Send us your results at [Discourse](http://discuss.contentmine.org/)
- Share the tutorial with others in your department or social network.
- Ask us your questions at [Discourse](http://discuss.contentmine.org/), via Email (contact@contentmine.org) or on Twitter ([@TheContentMine](https://twitter.com/TheContentMine))

## RESSOURCES

