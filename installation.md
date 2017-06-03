# ContentMine Software Installation

## Option 1: Install software locally

**Recommended for tech-savvy people.**

You can find more about how to install the different software parts at their GitHub repositories. Here the needed ones to run the tutorials:
- [getpapers](https://github.com/ContentMine/getpapers) (>=0.4.12)
- [norma](https://github.com/ContentMine/norma) (>=0.2.26) ([download the latest release](https://github.com/ContentMine/norma/releases))
- [ami](https://github.com/ContentMine/ami) ([download the latest release](https://github.com/ContentMine/ami/releases))
- [Python3](https://www.python.org/) (>=3.4.3) with the networkx (>=1.11), pandas (>=0.19.2), matplotlib (>=1.5.3) and numpy (>=1.11.3) modules.
- [Jupyter Notebook](http://jupyter.org/) (>=4.2.1)
- [pyCProject](https://github.com/ContentMine/pyCProject) (v.)

## Option 2: Use the Virtual Machine

**Recommended for beginners and workshop participants.**

In the virtual machine image, everything is pre-configured and running. This is a out of the box solution and is especially recommended for non-tech-savy people. You can find more information how to setup the virtual machine [here](https://github.com/ContentMine/workshop-resources/tree/master/software-tutorials/vms). Which virtual machine image you should use, is listed at the related tutorial or workshop documentation.

When the virtual machine has been started, you need to install pyCProject and upgrade numpy via pip. The superuser password is ```password```.

```bash
sudo pip install --upgrade numpy
sudo pip install pycproject
```

## Learn text data mining with the ContentMine tools

Here a collection of resources, to dive into text and data mining with our software and use the full power of it:
- Get a basic understanding of what a [CProject](https://github.com/ContentMine/workshop-resources/tree/master/software-tutorials/cproject) and [Scholarly HTML](https://github.com/ContentMine/workshop-resources/tree/master/software-tutorials/sHTML) is.
- [pyCProject](https://github.com/ContentMine/pyCProject): if you want to analyse the mined facts in Python, you should have a look at our Python wrapper for the [CProject](https://github.com/ContentMine/workshop-resources/blob/master/software-tutorials/cproject/README.md) file-structure.
- run through our [software tutorials](https://github.com/ContentMine/workshop-resources/tree/master/software-tutorials). This helps you to get used to our tools. The needed ones are:
	- [getpapers](https://github.com/ContentMine/workshop-resources/blob/master/software-tutorials/getpapers/README.md)
	- [norma](https://github.com/ContentMine/workshop-resources/blob/master/software-tutorials/norma/README.md)
	- [ami](https://github.com/ContentMine/workshop-resources/blob/master/software-tutorials/ami/README.md)
- You should also take a look at our [tutorials section](../../tutorials) in this repo.
- To keep up to date and explore the full knowledge base we have, visit our website [contentmine.org](http://contentmine.org/) and our [GitHub account](https://github.com/ContentMine) to find out more. 


