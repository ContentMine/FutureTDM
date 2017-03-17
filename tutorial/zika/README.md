# Tutorial: Zika

## SETUP
#### Pre-requisites

**Option 1: Install software locally (recommended)**

You can find more about how to install the different software parts at their pages - [getpapers](https://github.com/ContentMine/getpapers), [norma](https://github.com/ContentMine/norma/releases) and [ami](https://github.com/ContentMine/ami/releases). This setup is the one used to create the tutorials. Additionally you need the following software to execute the tutorial:
- [getpapers](https://github.com/ContentMine/getpapers) (0.4.12)
- [norma](https://github.com/ContentMine/norma) (0.2.26)
- [ami](https://github.com/ContentMine/ami)
- [Python3](https://www.python.org/) (3.4.3) with the networkx (1.11), pandas (0.19.2), matplotlib (1.5.3) and numpy (1.11.3) modules.
- [Jupyter Notebook](http://jupyter.org/) (4.2.1)
- [pyCProject](https://github.com/ContentMine/pyCProject) (v.)

**Option 2: Use the Virtual Machine**

- [Install the Virtual Machine](https://github.com/ContentMine/workshop-resources/tree/master/software-tutorials/vms) with the [Virtual Machine Image May 2016](https://drive.google.com/open?id=0B7pJKedx9b97LTBVRmEzbzJOVlU) and start it. The VM consists of:
- [getpapers](https://github.com/ContentMine/getpapers) (0.4.5)
- [norma](https://github.com/ContentMine/norma) (0.2.26)
- [ami](https://github.com/ContentMine/ami) (0.2.24)
- [Python3](https://www.python.org/) (3.2.3) and [IPython](http://ipython.org/) (4.1.1).

The virtual machine has older software installed, so the commands sometimes do not work in the exact same way as documented here. For example, getpapers needs no ```-q``` flag for the query-term. Keep that in mind, if some problems appear.

Before you can start, you neet to install pyCProject and upgrade numpy via pip. The superuser password is ```password```.

```bash
sudo pip install --upgrade numpy
sudo pip install pycproject
```

**Preparation**
- Run through the tutorials of [getpapers](https://github.com/ContentMine/workshop-resources/tree/master/software-tutorials/cproject), [norma](https://github.com/ContentMine/workshop-resources/tree/master/software-tutorials/norma) and [ami](https://github.com/ContentMine/workshop-resources/tree/master/software-tutorials/ami).
- Get a basic understanding of what a [CProject](https://github.com/ContentMine/workshop-resources/tree/master/software-tutorials/cproject) and [Scholarly HTML](https://github.com/ContentMine/workshop-resources/tree/master/software-tutorials/sHTML) is.

Before you start, go into the ```tutorials/zika``` directory in the shell. If you are in the root directory of this repository, just execute:
```bash
cd tutorials/zika
```
, and you are in the right folder.

## TUTORIAL

### Download all Zika publications available
The first step always is to get the needed data from the API's. For this we use [getpapers](https://github.com/ContentMine/workshop-resources/tree/master/software-tutorials/cproject), the ContentMine tool for getting papers via different Publisher-API's.

First we want to have a look, how many results we find for the search term "zika".

```bash
getpapers -q 'zika' -o zika
```
1126 papers are found in our case (14. 03. 2017).

To download then all available PDF's of the found scientific papers, we add an output folder via ```-o zika``` and add ```-p``` to tell that we want PDF's.

```bash
getpapers -q 'zika' -o zika -p
```

After the download, we want to have a look on the downloaded files in a tree-like directory view.

```bash
tree zika
```

For some of the found publications there is also an XML-file available. To download them, we have to add ```-x``` as a flag to the query. The results then can be viewed again with the tree command.

```bash
getpapers -q 'zika' -o zika -x
tree zika
```
The query finds 100 XML-files, and can download 98 of them (14. 03. 2017).

Finally to complete our dataset, we also download all supplementary materials available for the zika-publications. Simply add ```-s``` to the query, and view the results as usual.

```bash
getpapers -q 'zika' -o zika -s
tree zika
```
Of the 100 XML-files for 57 of them supplementary materials can be found, and all have been downloaded.

Now we have all the available data, which can be used for further analysis.

### Normalize the data

Before we can start with the extraction and analysis, we have to normalize the raw data and convert it to [Scholarly HTML](https://github.com/ContentMine/workshop-resources/tree/master/software-tutorials/sHTML).

For this, we convert the fulltext.xml files to scholarly.html files with [norma](https://github.com/ContentMine/workshop-resources/tree/master/software-tutorials/norma) and view the results.

```bash
norma --project zika -i fulltext.xml -o scholarly.html --transform nlm2html
tree zika
```

### Extract the needed facts

The prepared data now can be used to extract the facts via [ami](https://github.com/ContentMine/workshop-resources/tree/master/software-tutorials/ami)'s different plugins.

**Extract Species**

First we use the species plugin to get the genus and binomial nomenclature.

```bash
ami2-species --project zika -i scholarly.html --sp.species --sp.type genus
ami2-species --project zika -i scholarly.html --sp.species --sp.type binomial
ami2-species --project zika -i scholarly.html --sp.species --sp.type genussp
tree zika
```

**Extract word frequencies**

Second we use the word plugin to get frequencies of words inside a publication. 

```bash
ami2-word --project zika -i scholarly.html --w.words wordFrequencies
```

**Extract clinical trials**
soon to come...

## Analyse the data with Jupyter Notebook

The analysis of the extracted data is done with Python in a [Jupyter Notebook](http://jupyter.org/).

**Get the [Jupyter Notebook](tutorial-zika.ipynb).**

**Use the Jupyter Notebook:**

Start jupyter via:
```bash
jupyter notebook
```
This should let your browser open a new tab with the actual directory in it. Click on the ```tutorial-zika.ipynb``` file to open the jupyter notebook. Then you can execute cell by cell and adapt the notebook to your needs.

### Check co-occurences of entities

## FOLLOW UPS

- Do another tutorial from the FutureTDM project: [Statistics](tutorial/statistics) and [Libraries](tutorial/libraries)
- Learn more about the tools used with our [software tutorials](https://github.com/ContentMine/workshop-resources)
- [Contribute to this repository](../README.md#contribution)
- Send us your results at [Discourse](http://discuss.contentmine.org/)
- Share the tutorial with others in your department or social network.
- Ask us your questions at [Discourse](http://discuss.contentmine.org/), via Email (contact@contentmine.org) or on Twitter ([@TheContentMine](https://twitter.com/TheContentMine))

## RESSOURCES

- [ContentMine/Hypothes.is Proposal](http://riojournal.com/articles.php?journal_name=rio&id=8424)
- [Zika virus](https://en.wikipedia.org/wiki/Zika_virus)

All materials worked out in this repository where conducted within the EU Horizon2020 project **Future TDM - The Future of Text and Data Mining**, an EU Horizon2020 research project with participation of Open Knowledge International and ContentMine. 

<a href="http://futuretdm.eu/" title=""><img src="/assets/images/logo-futuretdm.png" alt="FutureTDM" height=50 /></a> <a href="http://contentmine.org" title=""><img src="/assets/images/logo-contentmine.png" alt="ContentMine" height=50 /></a> <a href="http://okfn.org/" title="Open Knowledge International"><img src="/assets/images/logo-okf.png" alt="Open Knowledge International" height=50 /></a>

All content and data is licensed under the [Creative Commons Attribution 4.0 International License](http://creativecommons.org/licenses/by/4.0/). All code is under the [MIT license](https://opensource.org/licenses/MIT).

<img src="/assets/images/logo-ccby.png" alt="Creative Commons by" width=100 />

