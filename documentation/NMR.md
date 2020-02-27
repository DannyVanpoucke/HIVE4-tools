# NMR
Although VASP does not incorporate *core*-electrons during total energy
calculations, it is still possible to calculate (approximately) the [chemical
shifts](https://cms.mpi.univie.ac.at/wiki/index.php/LCHIMAG). 

The NMR-tool of HIVE extracts the relevant chemical shifts from the OUTCAR
file and generates an NMR-spectrum for each of the atomic species in the system.
The NMR-spectrum is written as a 2 column text-file which can easily be visualized 
using excel, xmgrace, gnuplot, ... 
The options of the tool are controlled via a simple text-file. 

## Usage:
The NMR function is available in command-line mode only.

```
> hive.exe NMR OUTCAR InputFile
```
with
* OUTCAR    : The name of an OUTCAR-formatted file
* InputFile : A simple text-file containing the parameters. Note that the capitalization has to be followed.
    * INCLUDE_G    : Logical indicating if the G=0 contribution is included. \[**DEFAULT** = .TRUE. \]
    * INCLUDE_CORE : Logical indicating if the core contribution is included. \[**DEFAULT** = .TRUE. \]
    * SHAPE        : Peak-shape choice. (Delta, Gaussian) \[**DEFAULT** = Gaussian \]
    * SIGMA        : Peak width of Gaussian shaped peaks. One value per atomic species (POSCAR definition). \[**DEFAULT** = 1 ppm \]
    * SHIFT        : Do the NMR peaks need to be shifted? \[**DEFAULT** = No \]
		* No	  : No shifting.
        * Species : One value per atomic species
        * Atom    : One value for each separate atom.
    * SHIFT_VALUE : real valued shift(s) in ppm if Shift is not "No". \[**DEFAULT** = 0.0 \]
    * STEPSIZE    : real valued step-size of the grid on which the spectrum is presented \[**DEFAULT** = 0.1 (ppm)\] 

To get the most up-to-date information of this function, the build-in manual 
can accessed the usual way, via the command:
```
> hive.exe NMR?
```


## Acknowledgment
If you use this tool you should cite the following publication:
*"UV-Curable Biobased Polyacrylates Based on a Multifunctional 2 Monomer Derived from Furfural"*
Jules Stouten, Danny E. P. Vanpoucke, Guy Van Assche, and Katrien V. Bernaerts, 
*Macromolecules* **53(4)**, 1388-1404 (2020).
DOI: [10.1021/acs.macromol.9b02659](https://dx.doi.org/10.1021/acs.macromol.9b02659)


## Author
Danny E.P. Vanpoucke
  