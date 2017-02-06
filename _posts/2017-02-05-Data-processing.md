o---

layout: post
title: DDA Data Processing from Mass Spec
---

02/05/2017

### Data processing steps after Mass Spectrometry

I carried out all of my data processing by using `ssh` to remote login to Emu in the Roberts Lab. The following programs were installed to run the DDA proteomics analyses: Comet, Trans Proteomic Pipeline (Peptide and Protein Prophet), and Abacus. To use Jupyter Notebook to document my progress I tunnelled into Emu using the following procedure:

- Open a Git Bash terminal locally and enter the following code:

`ssh -N -L localhost:8000:localhost:7000 srlab@128.95.149.195` 

- Enter password when prompted

- Terminal is active but it won't return any command prompt. You have created a tunnel into Emu. To start ipython on Emu

- Open a new Git Bash terminal, but keep the first one open.

- Enter `ssh srlab@128.95.149.195`

- Enter password when prompted

- Enter `ipython notebook --no-browser --port=7000`

- Now you are remotely logged into Emu and have started ipython without the browser.

- Open a browser locally and enter `localhost:8000`

- This will open Jupyter in your browser on the Emu machine. It will prompt you for the token which you can find in the second Git Bash terminal you opened.

1) The MS creates .raw files (which I stored on Owl) and to run peptide searches in Comet you should convert the files into .mzXML files. I saved these files in a local directory on Emu. I did this for all my files by running the following code:

`for file in ~/Documents/rhonda2016oyster/trochophora/C_gigas_proteome2016/20161205Sample*.raw
do
no_path=${file##*/}
no_ext=${no_path%.raw}
WINEPREFIX=~/.wine32 wine ReAdW.2016010.msfilereader.exe "no_ext".mzXML
done`

See [Jupyter notebook](https://github.com/Ellior2/Fish-546-Bioinformatics/blob/master/analyses/DDA_2016/000-Remotelogin_filechange.ipynb)

2) Next you will run a program called Comet which will search your .mzXML files against a protein sequence database. For this step you will need three items:

- A protein database for your target organism, in my case a Crassostrea gigas proteome ([contigs.fasta.transdecoder.pep](http://gigaton.sigenae.org/ngspipelines/#!/NGSpipelines/Crassostrea gigas - GIGATON)) with the addition of three contaminant files ([contam.other](https://raw.githubusercontent.com/Ellior2/Fish-546-Bioinformatics/master/analyses/DDA_2016/contam.other), [contam.human](https://raw.githubusercontent.com/Ellior2/Fish-546-Bioinformatics/master/analyses/DDA_2016/contam.human), and [contam.bovin](https://raw.githubusercontent.com/Ellior2/Fish-546-Bioinformatics/master/analyses/DDA_2016/contam.bovin)). I added the contaminant files using the following code:

`!cat contam.bovin contam.human contam.other contigs.fasta.transdecoder.pep > contigs_contam.fasta.transdecoder.pep`

- Your .mzXML files in one directory (excluding blanks and QCs)

- A comet.params files which I downloaded from this [website](http://comet-ms.sourceforge.net/parameters/parameters_201601/). I chose the  comet.params.high-low high res MS1 and low res MS2 e.g. Velos-Orbitrap.

All these files need to be in the same directory. Comet will produce pep.xml files for all your samples.

I used the following code to conduct my searches:

`!/home/shared/comet/comet.2016012.linux.exe -PPcomet.params.high-low -Dcontigs_contam.fasta.transdecoder.pep 20161205_Sample_*.mzXML`

See [Jupyter notebook](https://github.com/Ellior2/Fish-546-Bioinformatics/blob/master/analyses/DDA_2016/001-Comet.ipynb)

3) Next I calculated statistics associated with the peptide to protein matches using Trans Proteomic Pipeline (TPP). I used a p-value cut off of 0.9. I used the pep.xml files for this step and kept everything in the same directory. this step will create a series of interact- files for each of your pep.xml files. The following code was used:

`!/usr/tpp_install/tpp/bin/xinteract -dDECOY_ -N20161205_sample_1 20161205_sample_1.pep.xml -p0.9 -OAp`

See Jupyter notebooks
[1](https://github.com/Ellior2/Fish-546-Bioinformatics/blob/master/analyses/DDA_2016/002-TPP_firstset.ipynb)
[2](https://github.com/Ellior2/Fish-546-Bioinformatics/blob/master/analyses/DDA_2016/002-TPP_secondset.ipynb)
[3](https://github.com/Ellior2/Fish-546-Bioinformatics/blob/master/analyses/DDA_2016/002-TPP_thirdset.ipynb)
[4](https://github.com/Ellior2/Fish-546-Bioinformatics/blob/master/analyses/DDA_2016/002-TPP_fourthset.ipynb)

4) Abacus correlates protein inferences across my sample files so that a single protein can be associated with each peptide. The output will be a compiled single .tsv file with corresponding spectral counts and normalized spectral abundance factor (NSAF) which is a proxy for protein abundance. 

I used the following code:

`!/usr/tpp_install/tpp/bin/ProteinProphet interact*.pep.xml interact-COMBINED.prot.xml`

I made an [Abacus parameter file](https://raw.githubusercontent.com/Ellior2/Fish-546-Bioinformatics/master/analyses/DDA_2016/Abacus_parameters.txt)

And used this code in the bash window:

`java -Xmx16g -jar /home/shared/abacus/abacus.jar -p ~/Documents/rhonda/Abacus_parameters.txt`

See [Jupyter notebook](https://github.com/Ellior2/Fish-546-Bioinformatics/blob/master/analyses/DDA_2016/006-Abacus.ipynb)

5) The next step will involve the Qspec spectral counter which is a web-based program found [here](http://www.nesvilab.org/qspec.php/). Input files need to be in .txt file format. This program finds differntially abundant proteins by giving you a log fold change and z-statistic for each protein. A protein is generally considered significant if it has a log fold change of at least absolute value of 0.5 and a z-stat of at least absolute value of 2.
