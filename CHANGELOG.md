# Change Log

# v1.0.0: public release

## v1.0.1: correct release
### Changed
- correction of the dump fit_struct in the .sav file to be human readable
- addition of the model_struct containing parameters best fit values and uncertainties in .sav file
- update of model library, correction of overflow problems in synchrotron laws

### Fixed
- correction of graphic bug in displaying the walker chains plot (inverted color depending on AF_cut value)

## v1.1.0: update release
### Changed 
- implementation of redshift as free parameters
- homogeneisation of examples to free parameter redshift implementation

## Fixed
- correction of various bugs

## v1.1.0.dev: Python3 development release
### Changed
- updated all ```print()``` statements
- moved helper modules to /project directory to resolve ImportError 
- Deprecated function astropy.analytic_functions.blackbody_nu replaced with
astropy.modeling.blackbody.blackbody_nu
- Reading and writing files in non-binary mode to prevent IO TypeError 
	
### Fixed
- yaml.load() warning suppressed by adding Loader arg

```fit_struct = yaml.load(input, Loader=yaml.FullLoader) ```
- Slicing convention of Astropy.table()