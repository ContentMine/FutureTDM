# Tutorial: Systematic Literature Review (Train the Trainees for Libririans)

## SETUP

**All software necessary can be found in [installation.md](../../installation.md).**

**Additional requirements**

- Memory: The downloaded data needs around 700 MB on your harddrive.

As preparation we recommend to have a look at the resources list in [installation.md](../../installation.md). 

## TUTORIAL

### Download from Europe PMC

The first step always is to get the needed data from the APIs. For this, we use [getpapers](https://github.com/ContentMine/workshop-resources/tree/master/software-tutorials/cproject), the ContentMine tool for getting papers via different Publisher APIs. In this tutorial, we will only use open access literature from [Europe PMC](http://europepmc.org/). We can search within their database of 3.5 million fulltext papers from the life-sciences. About one million of these are Open Access. Please refer to [Europe PMC-Data](http://europepmc.org/FtpSite) for details. This will take less than 200MB of memory.

**Get publications**

Then, we have a look at how many results we find for the query term. For further information on how to create more complex queries for the EUPMC API, read [here](https://github.com/ContentMine/getpapers/wiki/europepmc-query-format) or [here](https://github.com/ContentMine/workshop-resources/tree/master/software-tutorials/getpapers#complex-queries-for-europepmc).

```bash
getpapers -q $QUERY -o $FOLDER
```
1126 papers were found in this case (14. 03. 2017).

Then, we download the ```fulltext.xml``` files for each publication. For this, add ```-x``` flag to the query. The results can then be viewed again with the tree command.

```bash
getpapers -q $QUERY -o $FOLDER -x
tree zika
```

### Normalize the data

Before we can start with the extraction and analysis, we have to normalize the raw data and convert it to [Scholarly HTML](https://github.com/ContentMine/workshop-resources/tree/master/software-tutorials/sHTML), so it is easier to process further on. For this, we convert with [norma](https://github.com/ContentMine/workshop-resources/tree/master/software-tutorials/norma) the ```fulltext.xml``` files to ```scholarly.html``` files, and view the results.

```bash
norma --project zika -i fulltext.xml -o scholarly.html --transform nlm2html
tree zika
```

### Extract the needed facts

The prepared data now can be used to extract the facts via [ami](https://github.com/ContentMine/workshop-resources/tree/master/software-tutorials/ami)'s different plugins. This will be &mdash; besides the [metadata](https://en.wikipedia.org/wiki/Metadata) of the publications &mdash; the main datasource for the further analysis later on.

#### Extract Species

First, we use the [species plugin](https://github.com/ContentMine/workshop-resources/tree/master/software-tutorials/ami#ami2-species) to get the genus and binomial nomenclature.

```bash
FOLDER='zika'
ami2-species --project $FOLDER -i scholarly.html --sp.species --sp.type genus
ami2-species --project $FOLDER -i scholarly.html --sp.species --sp.type binomial
ami2-species --project $FOLDER -i scholarly.html --sp.species --sp.type genussp
tree zika
```

### Analyse the data with Jupyter Notebook

The analysis of the extracted data is done with Python in a [Jupyter Notebook](http://jupyter.org/). There are several methods applied. Some of them are descriptive and show the wanted outcome, but some are explorativ, and conclusions must be done by a domain expert by exploring the data and its presentation by her/himselves. The following analysis is done:
- 

**Get the [Jupyter Notebook: tutorial-systematic-literature-review.ipynb](tutorial-systematic-literature-review.ipynb).**

**Use the Jupyter Notebook:**

Go to the ```tutorials/systematic-literature-review/``` folder and start jupyter via:
```bash
jupyter notebook
```

This should let your browser open a new tab with the actual directory in it. Click on the ```tutorial-systematic-literature-review.ipynb``` file to open the jupyter notebook. Then you can execute cell by cell and adapt the notebook to your needs. There is a more detailed description of the analysis done in the Jupyter notebook.

## FOLLOW UPS

- Do another tutorial from the FutureTDM project: [Statistics](tutorial/statistics) and [Zika](tutorial/zika)
- Learn more about the tools used with our [software tutorials](https://github.com/ContentMine/workshop-resources)
- [Contribute to this repository](../README.md#contribution)
- Send us your results at [Discourse](http://discuss.contentmine.org/)
- Share the tutorial with others in your department or social network.
- Ask us your questions at [Discourse](http://discuss.contentmine.org/), via Email (contact@contentmine.org) or on Twitter ([@TheContentMine](https://twitter.com/TheContentMine))

## RESSOURCES

All materials worked out in this repository where conducted within the EU Horizon2020 project **Future TDM - The Future of Text and Data Mining**, an EU Horizon2020 research project with participation of Open Knowledge International and ContentMine. 

<a href="http://futuretdm.eu/" title=""><img src="/assets/images/logo-futuretdm.png" alt="FutureTDM" height=50 /></a> <a href="http://contentmine.org" title=""><img src="/assets/images/logo-contentmine.png" alt="ContentMine" height=50 /></a> <a href="http://okfn.org/" title="Open Knowledge International"><img src="/assets/images/logo-okf.png" alt="Open Knowledge International" height=50 /></a>

All content and data is licensed under the [Creative Commons Attribution 4.0 International License](http://creativecommons.org/licenses/by/4.0/). All code is under the [MIT license](https://opensource.org/licenses/MIT).

<img src="/assets/images/logo-ccby.png" alt="Creative Commons by" width=100 />
