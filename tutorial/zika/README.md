# Tutorial: Zika

**The tutorial shows you some basic and advanced text and data mining methods to explore the scientific publications and get a better understanding of the Zika virus.**

The main part will focus on getting information about the Zika virus, the research done about it and the most relevant entities for it. A typical way how to gather information about a [pandemic](https://en.wikipedia.org/wiki/Pandemic) is to have a look at:
- a) the virus itself ([Zika virus](https://en.wikipedia.org/wiki/Zika_virus))
- b) the virus-transmitting species (also known as [disease vectors](https://en.wikipedia.org/wiki/Vector_(epidemiology)); in our case [*Aedes aegypti*](https://en.wikipedia.org/wiki/Aedes_aegypti) and [*Aedes albopictus*](https://en.wikipedia.org/wiki/Aedes_albopictus))
- c) drugs, clinical trials and locations mentioned in combination with the virus and the virus-transmitting species
- d) similar pandemics/viruses (like the [Yellow fever](https://en.wikipedia.org/wiki/Yellow_fever) or the [Usutu virus](https://en.wikipedia.org/wiki/Usutu_virus), which is a flavivirus amongst a [range of suspects](https://wwwnc.cdc.gov/eid/article/22/12/16-0123-t2) for becoming the next pandemic)

As data source, we use all publications from the [Europe PMC](https://europepmc.org/) (EUPMC) API, because they are Open Access.

The used approach should also work as a blueprint to gather information about pandemics in general and help for future research when a new virus starts to spread.

## ABOUT ZIKA
The Zika virus (ZIKV) is a member of the virus family [Flaviviridae](https://en.wikipedia.org/wiki/Flaviviridae). It is spread by daytime-active [Aedes](https://en.wikipedia.org/wiki/Aedes) mosquitos, such as [Aedes aegypti](https://en.wikipedia.org/wiki/Aedes_aegypti) and [Aedes albopictu](https://en.wikipedia.org/wiki/Aedes_albopictus).

**Additional information**

- The [Spondweni virus](https://en.wikipedia.org/wiki/Spondweni_virus) is mentioned as phylogenetically very close to the Zika virus.

## SETUP
#### Pre-requisites

**All materials necessary, to setup your ContentMine software environment can be found at [FutureTDM README.md](../../README.md#preparation).**

**Requirements**

- Memory: The downloaded data needs around 700 MB on your harddrive.

**Preparation**

- Run through the tutorials of [getpapers](https://github.com/ContentMine/workshop-resources/tree/master/software-tutorials/cproject), [norma](https://github.com/ContentMine/workshop-resources/tree/master/software-tutorials/norma) and [ami](https://github.com/ContentMine/workshop-resources/tree/master/software-tutorials/ami). 
- Get a basic understanding of what a [CProject](https://github.com/ContentMine/workshop-resources/tree/master/software-tutorials/cproject) and [Scholarly HTML](https://github.com/ContentMine/workshop-resources/tree/master/software-tutorials/sHTML) is.

Both introductory steps are not mandatory, but help to better understand the tutorial and adapt it to your own needs.

Before you start, go into the ```tutorials/zika``` directory in the shell. If you are in the root directory of this repository, just execute:
```bash
cd tutorials/zika
```
, and you are in the right folder.

## TUTORIAL

### Download from Europe PMC

The first step always is to get the needed data from the APIs. For this, we use [getpapers](https://github.com/ContentMine/workshop-resources/tree/master/software-tutorials/cproject), the ContentMine tool for getting papers via different Publisher APIs. In this tutorial, we will mainly use open access literature from [Europe PMC](http://europepmc.org/). We can search within their database of 3.5 million fulltext papers from the life-sciences. About one million of these are Open Access. Please refer to [Europe PMC-Data](http://europepmc.org/FtpSite) for details. This will take less than 200MB of memory.

**Get Zika publications**

First, we want to set the variables for the query and for the folder we want the data to be stored in.

```bash
QUERY='zika'
FOLDER='zika'
```

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

**Get Aedes aegypti (virus-transmitting Mosquito) publications**

We then also want to have a look at all publications of the virus-transmitting Mosquito [Aedes aegypti](https://en.wikipedia.org/wiki/Aedes_aegypti) (```Stegomyia aegypti``` is a synonym for Aedes aegypti).

```bash
QUERY='stegomyia aedes aegypti'
FOLDER='aedesaegypti'
getpapers -q $QUERY -o $FOLDER -x
tree aedesaegypti
```

231 publications are found.

**Get Usutu virus publications**

At last, we want to have a look at the [Usutu virus](https://en.wikipedia.org/wiki/Usutu_virus) and download the related publications. This virus is amongst several dozens of known viruses that have been [found](https://doi.org/10.3201/eid2212.160123) to have a high epidemic potential. So maybe we can apply some lessons learned from the Zika virus to this corpus.

```bash
QUERY='usutu'
FOLDER='usutu'
getpapers -q $QUERY -o $FOLDER -x
tree usutu
```

193 publications are found.

Finally, we have all the available data, which can be used for further analysis.

**Optional: Get supplementary materials, if needed**

If you want to use the supplementary materials available, here is the command to download it. Simply add ```-s``` to the query, and view the results as usual.

```bash
getpapers -q 'zika' -o zika -s
tree zika
```

**Optional: Get the PDFs**

To download all PDFs of the scientific papers, we add ```-p``` to tell that we want PDFs. Please beware that this will take around 3GB of space on your harddrive.

```bash
QUERY='zika'
FOLDER='zika'
getpapers -q $QUERY -o $FOLDER -p
tree zika
```

**Save raw data**

At this point, we recommend to save the raw data, so you can jump back to this point if you want to later on. You can simply copy your three folders or compress them, whatever you like.

### Normalize the data

Before we can start with the extraction and analysis, we have to normalize the raw data and convert it to [Scholarly HTML](https://github.com/ContentMine/workshop-resources/tree/master/software-tutorials/sHTML), so it is easier to process further on. For this, we convert with [norma](https://github.com/ContentMine/workshop-resources/tree/master/software-tutorials/norma) the ```fulltext.xml``` files to ```scholarly.html``` files, and view the results.

```bash
norma --project zika -i fulltext.xml -o scholarly.html --transform nlm2html
tree zika
```

```bash
norma --project aedesaegypti -i fulltext.xml -o scholarly.html --transform nlm2html
tree aedesaegypti
```

```bash
norma --project usutu -i fulltext.xml -o scholarly.html --transform nlm2html
tree usutu
```

### Extract the needed facts

The prepared data now can be used to extract the facts via [ami](https://github.com/ContentMine/workshop-resources/tree/master/software-tutorials/ami)'s different plugins. This will be &mdash; besides the [metadata](https://en.wikipedia.org/wiki/Metadata) of the publications &mdash; the main datasource for the further analysis later on.

#### Extract Species

First, we use the [species plugin](https://github.com/ContentMine/workshop-resources/tree/master/software-tutorials/ami#ami2-species) to get the genus and binomial nomenclature. The species are especially important, because knowing them could give us a lead in terms of Zika-transmitting animals, in our case *Aedes* (mosquitos).

```bash
FOLDER='zika'
ami2-species --project $FOLDER -i scholarly.html --sp.species --sp.type genus
ami2-species --project $FOLDER -i scholarly.html --sp.species --sp.type binomial
ami2-species --project $FOLDER -i scholarly.html --sp.species --sp.type genussp
tree zika
```

```bash
FOLDER='aedesaegypti'
ami2-species --project $FOLDER -i scholarly.html --sp.species --sp.type genus
ami2-species --project $FOLDER -i scholarly.html --sp.species --sp.type binomial
ami2-species --project $FOLDER -i scholarly.html --sp.species --sp.type genussp
tree aedesaegypti
```

```bash
FOLDER='usutu'
ami2-species --project $FOLDER -i scholarly.html --sp.species --sp.type genus
ami2-species --project $FOLDER -i scholarly.html --sp.species --sp.type binomial
ami2-species --project $FOLDER -i scholarly.html --sp.species --sp.type genussp
tree usutu
```

#### Extract word frequencies

Second, we use the word plugin to get frequencies of words in a publication. This can help us to get a better understanding  of the most important concepts. This could be a re-occuring location, a method constantly used or an important animal in the transmission process. With this explorative approach, it is planned to find new relations or get a general understanding of important knowledge.

```bash
FOLDER='zika'
ami2-word --project $FOLDER -i scholarly.html --w.words wordFrequencies
tree zika
```

```bash
FOLDER='aedesaegypti'
ami2-word --project $FOLDER -i scholarly.html --w.words wordFrequencies
tree aedesaegypti
```

```bash
FOLDER='usutu'
ami2-word --project $FOLDER -i scholarly.html --w.words wordFrequencies
tree usutu
```

#### Extract clinical trial IDs

soon to come...

### Analyse the data with Jupyter Notebook

The analysis of the extracted data is done with Python in a [Jupyter Notebook](http://jupyter.org/). There are several methods applied. Some of them are descriptive and show the wanted outcome, but some are explorativ, and conclusions must be done by a domain expert by exploring the data and its presentation by her/himselves. The following analysis is done:
- plot a timeline of the publication years
- get the most mentioned words and species over the full corpus
- find relations between terms (species, words, authors, journals, publications) through network analysis methods, like community detection, co-occurences and network-projection.
- find all publications in which a term was mentioned

**Get the [Jupyter Notebook](tutorial-zika.ipynb).**

**Use the Jupyter Notebook:**

Start jupyter via:
```bash
jupyter notebook
```

This should let your browser open a new tab with the actual directory in it. Click on the ```tutorial-zika.ipynb``` file to open the jupyter notebook. Then you can execute cell by cell and adapt the notebook to your needs. There is a more detailed description of the analysis done in the Jupyter notebook.

## FOLLOW UPS

- Do another tutorial from the FutureTDM project: [Statistics](tutorial/statistics) and [Libraries](tutorial/libraries)
- Learn more about the tools used with our [software tutorials](https://github.com/ContentMine/workshop-resources)
- [Contribute to this repository](../README.md#contribution).
- Send us your results at [Discourse](http://discuss.contentmine.org/) or via Email (contact@contentmine.org).
- Share the tutorial with others in your department or on the web.
- Ask us your questions at [Discourse](http://discuss.contentmine.org/), via Email (contact@contentmine.org) or on Twitter ([@TheContentMine](https://twitter.com/TheContentMine)).

## RESSOURCES

- [ContentMine/Hypothes.is Proposal](https://doi.org/10.3897/rio.2.e8424)
- [Wikidata:WikiProject Source MetaData/Wikidata lists/Items about Zika virus or fever](https://www.wikidata.org/wiki/Wikidata:WikiProject_Source_MetaData/Wikidata_lists/Items_about_Zika_virus_or_fever)
- Article: [Zika may be spread by up to 35 species of mosquitoes, researchers say](http://www.miamiherald.com/news/health-care/article135414359.html)


All materials in this repository were produced within the EU Horizon2020 project **Future TDM - The Future of Text and Data Mining**, an EU Horizon2020 research project with participation of Open Knowledge International and ContentMine. 

<a href="http://futuretdm.eu/" title=""><img src="/assets/images/logo-futuretdm.png" alt="FutureTDM" height=50 /></a> <a href="http://contentmine.org" title=""><img src="/assets/images/logo-contentmine.png" alt="ContentMine" height=50 /></a> <a href="http://okfn.org/" title="Open Knowledge International"><img src="/assets/images/logo-okf.png" alt="Open Knowledge International" height=50 /></a>

All content and data is licensed under the [Creative Commons Attribution 4.0 International License](http://creativecommons.org/licenses/by/4.0/). All code is under the [MIT license](https://opensource.org/licenses/MIT).

<img src="/assets/images/logo-ccby.png" alt="Creative Commons by" width=100 />

