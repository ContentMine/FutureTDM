# Tutorial: Statistics


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
soon to come...

## FOLLOW UPS

- Do another tutorial from the FutureTDM project: [Zika](tutorial/zika) and [Libraries](tutorial/libraries)
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

