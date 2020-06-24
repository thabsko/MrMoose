# Mr.Moose v.1.1.0.dev
MrMoose stands for Multi-Resolution Multi-Object/Origin Spectral Energy distribution fitting procedure. In a nutshell, this code allows to fit user-defined models onto a set of multi-wavelength data using a Bayesian framework. The code is shared with multiple examples to demonstrate its capabilities and allow the user to adapt it more easily to their specific requirements. MrMoose is designed to permit user a large freedom in a user-friendly fashion, but not being user-opaque. The code can therefore handle blended sources, large variation in resolution, and even upper limits consistenly. It also generates a series of ouputs allowing for an quick interpretation of the results. The code is using the emcee package, and saving the emcee sampler object (.pkl) allowing users to tranfer the output to personnal graphical interface. 


## Table of contents:
* References
* Requirements 
* Installation
* Usage
* Known Issues
* Contributing
* Advanced features
* Tips and tricks


## References
If using this code, please refer to the published paper of the code:
(submitted to MNRAS, under reviewing process)
arxiv pdf: https://arxiv.org/pdf/1804.01748
doi: 10.1093/mnras/sty831

## Requirements
pathos>=0.2.0
tqdm>=4.8.4
scipy>=0.14.0
guppy3>=3.0.0
numpy>=1.9.1
emcee>=2.2.1
corner>=2.0.1
pycallgraph>=1.0.1
matplotlib>=1.5.1
astropy>=2.0rc1
PyYAML>=3.12

## Installation
Download MrMoose from github, either by running in a terminal (require git to be installed)
git clone https://github.com/gdrouart/MrMoose.git
(or as a standard .zip file from the same url in a browser)

Run the following in the directory, to install all required dependencies
```
python setup.py install
````

Add the path to MrMoose in your PYTHONPATH variable in your .bashrc or .profile to be called on demand
export PYTHONPATH=Your_path_to_MrMoose_directory:$PYTHONPATH

## Usage
We summarise here the first run of MrMoose. 

In an ipython for instance, enter:
```
run example_1.py
```

This will create three files, with the following path:
 - data/fake_source_ex1.dat
 - models/fake_source_ex1.mod
 - fake_source_ex1.fit

The .dat file contains all the data, the .mod file contains all the models (function calls) and
the interval to be considered for each parameter and the .fit file contains the setting to
perform the fit. 

To run your first fit, after launching ipython:
```
import mrmoose
tab = mrmoose.SED_fit('fake_source_ex1.fit')
```
will perform your first run and generate your first results! (several .pdf files and a .pkl file
in the outputs folder)

## Known Issues
- Initial values set as the median of the interval of parameters
- Require to underestimate the parameters(especially normalisation factor) in case of the presence of upper limits
- Parallelisation on one source only is not effective, but working efficiently for sample (one source per core)

## Contributing
- Implementation of checkpoints to re-start chain convergence in case of crash/stops
- Allowing different prior on the parameter (only uninformative, uniform prior in v1.0)
- Implement Jupyter interface
- Transform MrMoose in a package
- Implement use of the logging system
- Implement template libraries of non-linear models to be fit along
- Migration to Python 3
- Allowing different redshift for different components, and allowing redshift as a free parameter - added in Version 1.1
- Move the advanced feature to the setting file (.fit) as optional parameters

## Advanced Features
- AF_cut: in the mrmoose.py file, the option "AF_cut" can be modified to filter manually walkers below a
given acceptance fraction(AF) value. The default value is -1, where the code filter automatically chains
with AF<mean(AF)/2, but is not necessarily optimal in certain cases. To obtain a view of the distribution
of AF values, change the "histo" value to True (located just below the AF_cut). 
- histo: This will enable the plot of a histrogram of the AF values during the convergence plot procedure. 
- layout: in the mrmoose.py the layout option allow for different style: presentation and talk. Customisation
is possible by adding your own keyword and options - following the rcParams dictionary of matplotlib format -
in the mm_utilities.py file in the function named "format_plot_output".
- AICc(in development): a number to compare different model combination directly. See Akaike Information Criteria
definition for a description of this diagnostic tool for model comparison. 

## Tips and Tricks
We provide here some extra tips to manipulate ouputs:

To compress the pdf into more handy version:
 - pdf to compressed pdf
gs -sDEVICE=pdfwrite -dCompatibilityLevel=1.4 -dPDFSETTINGS=/ebook -dNOPAUSE -dQUIET -dBATCH -sOutputFile=output.pdf input.pdf
 - pdf to png (or jpeg), just play around with the density and resizing to obtain a good quality image much lighter! 
convert -density 200 -resize 200% input.pdf -quality 100 output.png
