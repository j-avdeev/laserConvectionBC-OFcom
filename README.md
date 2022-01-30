Forked from [laserConvectionBC by Tobias Holzmann](https://bitbucket.org/shor-ty/laserconvectionbc/src)

Works fine on OpenFOAM.org (>=9). For details use [testCase](https://github.com/j-avdeev/LaserCase)


# README #

This README includes the steps which are necessary to get this application up and running.

### OpenFOAM Versions ###
* Generated for version
** 4.x **
** 5.x **
** 9.x ** (file laserConvectionFvPatchField.C updated)

### What is this repository for? ###
* This repository provides a LASER boundary condition based on the Gaussian distribution function with additional convective heat transfer
* The user can specify an arbitrary amount of LASER sources within one patch
* The LASER Source can only be applied perpendicular to the x-y plane (no transformation added)
* In addition, each LASER source can be moved circularly or linearly
* Circular motion means to move the Gaussian spot around a center point with a given omega
* Linear motion means to move the Gaussian spot linear within a set of given points with a defined linear velocity

### How do to compile the library and set-up the boundary condition? ###
* Feel free to compile it where ever you want, but normally its nice to have a fixed folder for _user compiled stuff_
* Make a new folder
> mkdir -p $FOAM_RUN/../OpenFOAM_extensions
* Switch to the new folder
> cd $FOAM_RUN/../OpenFOAM_extensions
* Clone the repository to the new folder
> git clone https://shor-ty@bitbucket.org/shor-ty/laserconvectionbc.git
* Switch to the repository directory
> cd laserconvectionbc
* After that pull it
> git pull
* Now you have your libraries available and you can start compiling
> wmake libso
* Compiling finished
* A description how to set-up the boundary condition in your T-File is given in the header file

### Using the library ###
* If you compiled the library (as explained above) you have to add the following line to your controlDict
> libs ( "liblaserConvectionBC.so" );
* After that the boundary condition should be available

### Using the BC within a special solver (not compiled as a stand alone library, offers more coupling but is only valid for this solver)
* For that go to the following file
> laserConvectionFvPatchField.H
* Uncomment the last lines that are commented
```C++
// Only needed if you compile with your solver
#ifdef NoRepository
#     include "laserConvectionFvPatchField.C"
#endif
```
* Go to the solver that you want to couple with the boundary condition
* Add the boundary source file to your solver by adding the source file (and path) to the 'Make/files' file of your solver. It should look somehow like that (the first and last character is just for highlighting and should not be in the file):
```bash
'../../fvPatchFields/laserConvectionBC/laserConvectionFvPatchFields.C'
../../fvPatchFields/AOPCTractionDisplacement/AOPCTractionDisplacementFvPatchVectorField.C
../../fvPatchFields/fixedDisplacement/fixedDisplacementFvPatchVectorField.C
AOPCHeatTreatmentFoam.C

EXE = $(FOAM_USER_APPBIN)/AOPCHeatTreatmentFoam
```
* Compile your solver
* Done


### Usage as BC ###
* In the header file you will find an example, how to set-up the boundary condition

### Contribution guidelines ###
* If you have questions, hints or any suggestions please email me to Tobias.Holzmann@Holzmann-cfd.de

### Warranty ###
* There is no warranty that the boundary works as expected

### Acknowledgement ###
*Financial support by the Austrian Federal Government (in particular from Bundesministerium fuer Verkehr, Innovation und Technologie and Bundesministerium fuer Witschaft, Familie und Jugend) represented by Oesterreichische Forschungsfoerderungsgesellschaft mbH and the Styrian and the Tyrolean Provincial Government, represented by Steirische Wirtschaftsfoerderungsgesellschaft mbH and Standortagentur Tirol, within the framework of the COMET Funding Programme is gratefully acknowledged.
