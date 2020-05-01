# phononDefect
Command to perform phonon-related calculations based on the dynamical
matrix of a system. The subprogram requires a VASP formatted DYNMAT
file and POSCAR file to be present in the current folder.


The details of how the full brillouin zone dynamical matrix is constructed is 
discussed in <B>[\[1\]](#paper2_PhonDef)</B>.

## Usage:
The phonons subprogram is available in command-line mode only.
```
   > Hive.exe phonons INPUTFILE
```
with :
* INPUTFILE: the filename of the file containing the list of input parameters and their values.


### List of parameters:
--------------------
1. **General**
	* datasource : string providing the program which generated the
                  input data. Current options: VASP. (**DEFAULT**=VASP)
	* ncores     : Integer indicating the number of threads that should
                  be used for parallel single-node calculation (**DEFAULT**=1)
	* energy unit: Unit to use when writing the data: THz, 2PiTHz,
                  cm-1, meV. (**DEFAULT**=THz)
	* distance in points : logical parameter indicating if for the
                  band-plot use the actual distance in the reciprocal
                  space (false) or #q-points (true) (**DEFAULT**=.FALSE.)
	* subsystem  : Logical indicating if the input system is a subsystem
                  such as a point-defect, surface,...<br />
                  The "*active/participating*" atoms are indicated by the
                  selective dynamics option of the accompanying POSCAR.
                  (**OPTIONAL**, **DEFAULT**=.FALSE.)
	* subhessiantype: Integer value indicating how the Hessian for a sub-system
                  should be constructed and used. This parameter is
                  only read if subsystem = .TRUE.
                  (**OPTIONAL**, **DEFAULT**=0)
		- 0 : The full Hessian is retained, sanity checks are limited to
                the rows and columns linked to at least 1 subsystem atom.
		- 1 : The Hessian is reduced to the subsystem only. However,
                sanity checks are still performed on the full system (*cf.,* 0)
                as a way to allow for interactions between the subsystem and
                the frozen remainder. This allows for long ranged impacts on
                the subsystem.
		- 2 : The Hessian in reduced to the subsystem only, and sanity
                checks are limited to the subsystem only as well.
                Interactions are limited to the subsystem.
	* supercell  : Logical indicating if the input data is super-cell
                  data and need to be treated that way. (**DEFAULT**=.FALSE.)
                  If this keyword is set to true, also the keywords *cells*,
                  *nrunitatoms* and *unitatomlist* need to be given.
	* reducedDYNMAT: Logical indicating if the dynamical matrix is generated
                  for the reference atoms only (.TRUE.) or for all atoms in
                  the system(.FALSE.).
                  (**DEFAULT**=.TRUE. *if supercell=.TRUE., else .FALSE.*)
	* reducedDOS : Logical indicating if the DOS of a supercell should be
                  calculated using the Brillouin zone and bands of the
                  supercell (.false.) or those of the unit-cell(.true.).
                  Both approaches should give the same result, however,
                  their computational cost is located in different places:
		* supercell=more bands=bigger hessian to solve
		* unit-cell=bigger Brillouin zone=more q-points <br />
	**IMPORTANT**: *A consequence of using the reducedDOS is the
                      fact that the vibrational properties are calculated
                      for a cell the size of the unitcell used in the
                      reduced DOS. Consider this when providing GS energy.*
                  \[**Requires supercell=.true.**\](**DEFAULT=.FALSE.)
	* cells      : 3 integers indicating the multiplication of the unit-cell
                  along the *x*,*y*, and *z* lattice vectors, respectively.
                  (*Only read if supercell = .true.*)
	* nrunitatoms: Integer indicating the number of atoms in the unit-cell.
                  (*Only read if supercell = .true.*)
	* unitatomlist: List of integer values representing the atoms in the
                  reference unit-cell, given on a single line. (*Only read if
                  supercell = .true.*)
	* cleanup    : The Hessian matrix numerically produced may contain a lot
                  of noise. With this option you can select specific clean-up
                  options to be used. The matrix is symmetrized by default to
                  produce more clean zero's for the translational modes.
                  Additional clean-up can be done for
		* rot3D: project out the 3 rotational modes of a molecule
	* rotationprojection : Use the Tamkin or Gaussian approach to generating the
                  rotational modes. This keyword is only read if cleanup is set.
                  (**DEFAULT**=smallrot)
		* smallrot : the small-rotations way
		* gaussian : the gaussian way
	* ModifiedGramSchmidtAll : Logical if all vectors are orthogonalised using MGS.
                  This keyword is only read if cleanup is set. (**DEFAULT**=.TRUE.)

2. **GammaPhonons**
	* GammaPhonon: logical parameter indicating if the Gamma-point phonon
                  needs to be calculated. Options: .true., .false.
                  (**DEFAULT**=.TRUE.)

3. **band structure**
	* bands      : logical parameter indicating if a phonon band-structure
                  needs to be calculated. Options: .true., .false.
                  (**DEFAULT**=.FALSE.)
	* q-lines    : integer number giving the number of high symmetry lines
                  defined. Only read if bands=.true. (**DEFAULT**=1)
	* q per line : integer number >=2 giving the number of q-points per high
                  symmetry line. Only read if bands=.true. (**DEFAULT**=10)
	* q line list: This line is followed by a list of start and end points
                  of the high-symmetry q-lines.
                  First line gives the starting-point in units b1, b2 and b3,
                  and the second line the end point in units b1, b2 and b3
                  (*i.e.*, reciprocal fractional coordinates).
                  Every q-line is separated by a blank line
                  (**DEFAULT**= Gamma-L line)
	* q-path     : string giving the q-path. (**DEFAULT**= / )
		- *example 1:* K-G-L
           2 lines, first going from K to Gamma, second from Gamma to L
		- *example 2:* K-G|X-W
           2 lines, first going from K to Gamma, second from X to W

4. **Density of States**
	* dos        : logical parameter indicating if a phonon dos needs
                  to be calculated. Options: .true., .false.
                  (**DEFAULT**=.FALSE.)
	* dos density: measure of the number of q-points along the shortest
                  cartesian direction.(**DEFAULT**=10)
                  **NOTE:** *If this value is set to zero, then only the Gamma point
                  is considered.*
	* dostype    : type of dosgrid to use (**OPTIONAL**, **DEFAULT**=full)
                  If dos density is set to 0, then this option is
                  set to dostype=gamma.
		* full : A 3D grid is spanned over the first Brillouin zone.
		* gamma: Only the Gamma-point is considered (sets dos density to 0)
		* ...  : future to be implemented options.
	* dosgrid    : number of gridpoints in the phonon-DOS (**DEFAULT**=301)
	* include imaginary : logical indicating if imaginary frequencies are
                  to be included in the DOS.(**DEFAULT**=.FALSE.)
	* mindos     : user defined lower boundary of the DOS in units given
                  by "energy unit" (**DEFAULT**=0.0 or 1.1\*lowest negative
                  frequency if "*include imaginary = .true.*")
	* maxdos     : user defined upper boundary of the DOS in units given
                  by "*energy unit*" (**DEFAULT**=1.1\* highest value in the DOS)
	* smearing   : logical indicating if the DOS needs to be softened with
                  gaussian smearing.(**DEFAULT**=.FALSE.)
	* smearing width: width of the smearing in "*energy unit*". This
                  parameter is read only if smearing = .true.
                  (**DEFAULT**= value equivalent to 1 meV)
	* collect imaginary modes : logical indicating if the eigenmodes
                  of the imaginary frequencies at the worst case q-point
                  need to be extracted. (**DEFAULT**=.FALSE.)
	* partial dos : logical parameter indicating if the partial dos needs
                  to be calculated. It requires the "*dos*" option to be
                  switched on. Options: .true., .false. (**DEFAULT**=.FALSE.)

5. **Vibrational Contributions**
	* vibrational contributions : logical parameter indicating if
                  vibrational properties need to be calculated.
                  (**DEFAULT**=.FALSE.)
	* GS energy  : Real value that can be used to provide the DFT
                  ground state energy in eV (**DEFAULT**= 0.0).
                  **NOTE:** *In case reducedDOS=.true. the value provided
                        should be that of the reduced cell.*
	* vibrational source : Define which DOS will be used to calculate
                  the vibrational contributions.
                  options: gamma, full, or both.
                  If either "gamma" or "both" is chosen, then GammaPhonon
                  is set to true. If either "full" or "both" is chosen,
                  then dos is set to true.
                  (**DEFAULT**=gamma)
	* Tmin       : Lower bound of the temperature range for the vibrational properties.
	* Tmax       : Upper bound of the temperature range for the vibrational properties.
	* dT         : Stepsize in the temperature.

6. **Special Q-point of interest**
	* singleQ : logical indicating if we will be working with a special
               Q-point (**DEFAULT**=.FALSE.)
	* singleQcoord : 3 real values indicating the coordinates of the
               Q-point in reciprocal space. (Generally taken from output
               of a previous full phonon calculation. As such they should
               be actual reciprocal Q-point coordinates, unlike the
               Q-points used for band structures.)
              (**DEFAULT**= Gamma-point)
	* writeQmodes : String indicating which Q-modes need to be written.(**DEFAULT**=none)
		* none : nothing needs to be written
		* all  : write all modes
		* imag : write only the imaginary modes
		* XXX  : integer value indicating the specific mode number to write
	* writeDisplacement : logical indicating if a file containing the
              atomic displacements of a mode needs to be written.
              The modes of interest are also defined by writeQmodes.
              (**DEFAULT**=.FALSE.)
	* images : Integer giving the number of images that should be generated
              for a full phase cycle (2pi).
              (**DEFAULT**=36)
	* modeT  : Real value giving the temperature for the Bose-Einstein
              distribution used to define the amplitude of the phonon.
              This option is optional, if not present, then the alter-
              native definition for the amplitude is used.
              (**DEFAULT**= 300 K, if erroneous value is given)
	* scaleDisp : Real valued factor which can be used to additionally
              scale the atomic displacements.
              (**DEFAULT**=1.0)

7. **Parameters related to output-format**
	* bandformat : String parameter giving the output format type of
                  band structure data.<br /> 
				  **Options:**  (**DEFAULT**=column)
		* column : each band is written as a column in a space-
                       separated format. First column gives the length
                       along the line-path.
		* single : 2-column format (single input of xmgrace) with
                       the first column the position along the line path
                       and second the value of the specific band.
                       Different bands are separated by a blank line.
		* grace  : band, interval and batch-files as one would obtain
                       with the [bandgrabber module](bandgrabber.md) when investigating
                       electronic band structures.
		* EIGENVAL:write the electronic structure data in a file
                       using the VASP EIGENVAL-format.
            

General output and information on the flow of the calculation is written
to the **PHONONOUT.hive** file.


## Acknowledgment
If you use this tool you should cite the following publication:
* <a name="paper2_PhonDef">\[1\]<a> *"Partitioning the vibrational spectrum: Fingerprinting defects in solids"*,</br>
Danny E. P. Vanpoucke, 
*Computational Materials Science* **181**, 109736 (2020).</br>
DOI: [10.1016/j.commatsci.2020.109736](https://dx.doi.org/10.1016/j.commatsci.2020.109736)


## Author
Danny E.P. Vanpoucke
