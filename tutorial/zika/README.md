# Tutorial: Zika

**The tutorial shows you some basic and advanced text and data mining methods to explore the scientific publications and get a better understanding of the Zika virus.**

The main part will focus on getting information about the zika virus, the research done about it and the most relevant entities for it. A typical way how to gather information about a [pandemic](https://en.wikipedia.org/wiki/Pandemic) is to have a look on:
- a) the virus itself ([Zika virus](https://en.wikipedia.org/wiki/Zika_virus))
- b) the virus-transmitting species (in our case [Aedes aegypti](https://en.wikipedia.org/wiki/Aedes_aegypti) and [Aedes albopictu](https://en.wikipedia.org/wiki/Aedes_albopictus))
- c) drugs, clinical trials and locations mentioned in combination with the virus and the virus-transmitting species
- d) similar pandemics/viruses (like the [Yellow fever](https://en.wikipedia.org/wiki/Yellow_fever) or the [Usutu virus](https://en.wikipedia.org/wiki/Usutu_virus), which is under suspect of beeing the next pandemic)

As data source we use all publications from the [Europe PMC](https://europepmc.org/) (EUPMC) API, because they are Open Access.

The shown approach should also work as a blueprint to gather information about pandemics in general and help to gather needed information when, for example, a new virus starts to spread.

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

Before you start, go into the ```tutorials/zika``` directory in the shell. If you are in the root directory of this repository, just execute:
```bash
cd tutorials/zika
```
, and you are in the right folder.

## TUTORIAL

### Download from Europe PMC
The first step always is to get the needed data from the API's. For this we use [getpapers](https://github.com/ContentMine/workshop-resources/tree/master/software-tutorials/cproject), the ContentMine tool for getting papers via different Publisher-API's. This will take less than 200MB of memory.

**Get Zika publications**

First we want to set the variables for the query and for the folder we want the data to be stored in.

```bash
QUERY='zika'
FOLDER='zika'
```

Then we have a look, how many results we find for the query term. For further information on how to create more complex queries for the EUPMC API, read [here](https://github.com/ContentMine/getpapers/wiki/europepmc-query-format).

```bash
getpapers -q $QUERY -o $FOLDER
```
1126 papers are found in our case (14. 03. 2017).

Then we download the fulltext.xml files for each publication. For this, add ```-x``` flag to the query. The results then can be viewed again with the tree command.

```bash
getpapers -q $QUERY -o $FOLDER -x
tree zika
```
The query finds 100 XML-files, and can download 98 of them (14. 03. 2017).

**Get Aedes aegypti (virus-transmitting Mosquito) publications**

We then also want to get all publications of the virus transmitting Mosquito [Aedes aegypti](https://en.wikipedia.org/wiki/Aedes_aegypti) (```Stegomyia aegypti``` is a synonym for Aedes aegypti).

```bash
QUERY='Stegomyia aedes aegypti'
FOLDER='aedesaegypti'
getpapers -q $QUERY -o $FOLDER -x
tree aedesaegypti
```

231 publications are found.

**Get Usutu virus publications**

At last, we want to have a look on the [Usutu virus](https://en.wikipedia.org/wiki/Usutu_virus) and download the related publications. 

```bash
QUERY='usutu'
FOLDER='usutu'
getpapers -q $QUERY -o $FOLDER -x
tree usutu
```

193 publications are found.

**Optional: Get supplementary materials, if needed**

If you want to also use the supplementary materials available (takes a fair amount of memory), here is the command to download it. Simply add ```-s``` to the query, and view the results as usual.

```bash
getpapers -q 'zika' -o zika -s
tree zika
```
Of the 100 XML-files, for 57 of them supplementary materials can be found, and all of the 57 can be downloaded.

Finally, we have all the available data, which can be used for further analysis.

**Optional: Get the PDF's**

To download all PDF's of the found scientific papers, we add an output folder via ```-o zika``` and add ```-p``` to tell that we want PDF's. Please beware of, that this will take around 3GB of space on your harddrive.

```bash
QUERY='zika'
FOLDER='zika'
getpapers -q $QUERY -o $FOLDER -p
```

After the download, we want to have a look on the downloaded files in a tree-like directory view.

```bash
tree zika
```

**Save raw data**

At this point, we recommend to save the raw data, so you can jump back to this point, if you want to later on. You can simply copy your three folders or compress them, whatever you like.

### Normalize the data

Before we can start with the extraction and analysis, we have to normalize the raw data and convert it to [Scholarly HTML](https://github.com/ContentMine/workshop-resources/tree/master/software-tutorials/sHTML).

For this, we convert with [norma](https://github.com/ContentMine/workshop-resources/tree/master/software-tutorials/norma) the fulltext.xml files to scholarly.html files, and view the results.

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

The prepared data now can be used to extract the facts via [ami](https://github.com/ContentMine/workshop-resources/tree/master/software-tutorials/ami)'s different plugins.

**Extract Species**

First we use the species plugin to get the genus and binomial nomenclature.

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

**Extract word frequencies**

Second we use the word plugin to get frequencies of words inside a publication. 

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
- [Wikidata:WikiProject Source MetaData/Wikidata lists/Items about Zika virus or fever](https://www.wikidata.org/wiki/Wikidata:WikiProject_Source_MetaData/Wikidata_lists/Items_about_Zika_virus_or_fever)
- Article: [Zika may be spread by up to 35 species of mosquitoes, researchers say](http://www.miamiherald.com/news/health-care/article135414359.html)


All materials worked out in this repository where conducted within the EU Horizon2020 project **Future TDM - The Future of Text and Data Mining**, an EU Horizon2020 research project with participation of Open Knowledge International and ContentMine. 

<a href="http://futuretdm.eu/" title=""><img src="/assets/images/logo-futuretdm.png" alt="FutureTDM" height=50 /></a> <a href="http://contentmine.org" title=""><img src="/assets/images/logo-contentmine.png" alt="ContentMine" height=50 /></a> <a href="http://okfn.org/" title="Open Knowledge International"><img src="/assets/images/logo-okf.png" alt="Open Knowledge International" height=50 /></a>

All content and data is licensed under the [Creative Commons Attribution 4.0 International License](http://creativecommons.org/licenses/by/4.0/). All code is under the [MIT license](https://opensource.org/licenses/MIT).

<img src="/assets/images/logo-ccby.png" alt="Creative Commons by" width=100 />

