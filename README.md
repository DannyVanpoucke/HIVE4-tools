# HIVE-tools v4.x
Post-processing tool-set for *ab-intio* calculations obtained with [VASP](https://www.vasp.at/).

## History
Version 4.x of the HIVE-toolbox is the public version of the HIVE-toolbox version 3.x 
(the development version). The program is called HIVE which stands for **H**umble **I**nterface 
for **V**asp output**E**diting, which traces back to its original purpose. This software was
developed part as hobby-project, part as a necessary toolbox for analyzing first-principles
results during various scientific projects. During its first incarnation (2005-2009), 
the HIVE-toolbox consisted simply of the combination of multiple small fortran 95 tools 
through a common main loop. During a second incarnation (starting end 2009) the functions and 
subroutines were upgraded to take a more object-like approach (Fortran 2003 classes). At the
same time, a doxygen documentation was included. Over the following years the HIVE-toolbox was 
further extended to include more and more functionality. With the advent of version 4, I aim
to make the HIVE-toolbox publicly available,<sup>[1](#ftnoteFree)</sup> while at the same time 
clean up the code.<sup>[2](#ftnoteClean)</sup>

## Installation
1. Just copy the correct executable (Windows or linux-HPC) to a suitable location and add 
it to the path. (You might want to rename the executable to a more convenient name such as "hive4")
2. Place a copy of the license file and the manual file in the folder of your executable.
3. Try to run the executable via the commandline (dos-box in windows). If unsuccesful please 
report the error message via a Bug-report.

## Usage
This is a command-line program. As such it should be accessed via a terminal under 
unix-systems and a dos-box under windows. In windows, you can also use the program 
in your Cygwin installation, again approaching it through a terminal application 
(*e.g.*, xterm). 

## Errors, Bugs and other Nasties
In case you run into problems with the program please consult the following:
- [FAQ](/documentation/FAQ.md): problems with installation, running the program, finding information, crashes
- [Known Bugs](/documentation/Bugs.md): Although I strive to make the program bug-free, 
this will be the place to find more information on the status of currently know bugs. 

In case you run into a problem not mentioned in either of the above, please inform me via a Bug-report 
submitted as an issue. 


## Registration
Stemming from my personal curiosity, I would like to know for which purpose people are 
interested in using my program. In addition, it as also cool to keep track of how many people 
are using my program (wouldn't you?). So please drop me a line if you are downloading and 
using the HIVE-toolbox.<sup>[3](#ftnoteGDPR)</sup>   

## The Tools
A log of all changes between versions can be found [here](/documentation/changelog.md)
The list of implemented tools so far:
- [x] Extracting chemical shifts and generating [NMR spectra](/documentation/NMR.md). 
(*cf.*, paper [\[1\]](#paper1_NMR) )
- [ ] Calculation of phonons in periodic solids (and molecules)
- [x] Generation of [phonon spectra of (point) defects in periodic solids](/documentation/phononDefect.md). 
(*cf.*, paper [\[2\]](#paper2_PhonDef) )
- [ ] Hirhfeld-I for periodic materials


For further information please refer to my [webpage](https://dannyvanpoucke.be). 



## License
HIVE-tools is freely available for academic usage. As it is in constant development the license 
is limited to 1 year. This way you always have the most up-to-date version. You are free to use
it, but not to distribute (just send the link to this git-repository if you want to share it)
or sell it. If you like the HIVE-toolbox enough to use it for your work and use its results in 
published work, I would be grateful if you cite the relevant publication related to the used
tools (*cf.*, build-in manual and specific documentation).
    
The current version is valid until **31/12/2020**.


## Footnotes
<a name="ftnoteFree">1</a> The HIVE-toolbox is free (as in *free beer*), but not open-source.

<a name="ftnoteClean">2</a> Note that not a single part of the HIVE-toolbox was developed as subject 
of a funded scientific project. This has the unfortunate side-effect that too often code is 
implemented to work for the problem at hand. With the intended cleanup, some of the issues 
for more general problems will be resolved. 

<a name="ftnoteGDPR">3</a> In a world of overkill (called GDPR), I assume that by informing me of
your usage of the HIVE-toolbox, you grant me the right to keep this information in a list as long
as the HIVE-toolbox is available. I promise not to spam you with commercials, nor sell this information
for commercial purposes ;-) . 

## Bibliography
* <a name="paper1_NMR">\[1\]<a> *"UV-Curable Biobased Polyacrylates Based on a Multifunctional 2 Monomer Derived from Furfural"*,</br>
Jules Stouten, Danny E. P. Vanpoucke, Guy Van Assche, and Katrien V. Bernaerts, 
*Macromolecules* **53(4)**, 1388-1404 (2020).</br>
DOI: [10.1021/acs.macromol.9b02659](https://dx.doi.org/10.1021/acs.macromol.9b02659)

* <a name="#paper2_PhonDef">\[2\]<a> *"Partitioning the vibrational spectrum: Fingerprinting defects in solids"*,</br>
Danny E. P. Vanpoucke, 
*Computational Materials Science* **XX(Y)**, ZZ-ZZ (2020).</br>
DOI: [XX](https://dx.doi.org/XX)
