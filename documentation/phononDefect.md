# phononDefect
Vibrational spectra provide a very powerful tool for the structural investigation of
materials. Most quantum chemical and ab initio solid state codes provide a way of
generating the hessian matrix. Although for molecular and 0D systems this provides the
full vibrational spectrum, in case of a solid a dynamical matrix (an extended version of
the hessian matrix) is required for each point of the Brillouin zone. The [phonons](phonons.md) 
subprogram of HIVE provides the capacity to construct the vibrational spectrum over the 
entire 3D Brillouin zone. It also allows for the generation of an atom-projected phonon DOS. 

Using the output of the [phonons](phonons.md) subprogram, the phononDefect subprogram
allows you to generate the phonon DOS of a defect. This subprogram analyses the atom-projected 
phonon spectra for a system with the aim of extracting the spectrum of a defect. To do this 
you need to have the phonon spectrum of the bulk host system as well as the
spectrum of the system with the defect. The details of the approach are discussed
in <B>[\[1\]](#paper2_PhonDef)</B>. The resulting spectra are written to a multicolumn file
which can easily be visualized using excel, xmgrace, gnuplot, ... 

The options of the subprogram are controlled via a simple text-file. 

## Usage:
The phononDefect subprogram is available in command-line mode only.

```
> hive3.exe phononDefect INPUTFILE
```
with
* INPUTFILE  : a text file containing the parameters needed.
	* HOSTTDOS   : File containing the total DOS of the host system.
	* DEFECTTDOS : File containing the total DOS of the defect system.
	* DEFECTPDOS : File containing the projected DOS of the defect system.
	* POSCAR     : File containing the POSCAR data of the defect system.
                      \[**OPTIONAL**, **DEFAULT** = POSCAR \]
	* THRESHOLD  : Real valued maximum % of overlap for a "defect atom".
                      Out of range values are set to the corresponding bound.
                      \[**OPTIONAL**, **DEFAULT** = 50.0%\]
	* MAX_RADIUS : Real valued maximum radius (in Angstrom) to belong to defect system.
                      The minimal possible range is set to 0.01 Angstrom.
                      \[**OPTIONAL**, **DEFAULT** = 100A \]
	* FITTOHOST  : Logical indicating if the defect DOS spectra should be fit to the total DOS
                      of the host system (*i.e.* to negate lattice expansion due to small cell)
                      \[**OPTIONAL**, **DEFAULT** = .FALSE.\]
					  
To get the most up-to-date information of this function, the build-in manual 
can accessed the usual way, via the command:
```
> hive.exe phononDefect?
```

## Acknowledgment
If you use this tool you should cite the following publication:
* <a name="paper2_PhonDef">\[2\]<a> *"Partitioning the vibrational spectrum: Fingerprinting defects in solids"*,</br>
Danny E. P. Vanpoucke, 
*Computational Materials Science* **XX(Y)**, ZZ-ZZ (2020).</br>
DOI: [XX](https://dx.doi.org/XX)


## Author
Danny E.P. Vanpoucke
  