% redo-ifchange(1) Redux User Manual 
% Gyepi Sam
% January 23, 2014 

<!-- DO NOT EDIT -- Autogenerated file -->


#NAME

ifchange - Creates dependency on targets and ensure that targets are up to date.

#SYNOPSIS

redux ifchange [TARGET...]

#OPTIONS

  -?=false: Show help

  -h=false: Show help

  -help=false: Show help



#NOTES


The ifchange command creates a dependency on the target files and ensures that
the target files are up to date, calling the redo command, if necessary.

The current file will be invalidated if a target is rebuilt.


#DESCRIPTION

This command can be invoked as `redux ifchange` or, through a symlink, as `redo-ifchange`.

The `redo-ifchange` command is used in a `.do` script.

When the `.do` script for a target A contains the line `redo-ifchange B`, 
this means that the target A depends on B and A should be rebuilt if B changes. 

This command should be placed in a `.do` script and should not be run directly.

#DETAILS

Conceptually, redo-ifchange performs three tasks.

First, it creates a prerequisite record between A and B so A can track changes to B.
Second, it creates a dependency record between B and A so a change in B immediately invalidates  A.
Finally, if B is out of date, redo-ifchange ensures that B is made up to date.

B is considered out of date if it does not exist, is not in the database, is flagged as out of date, 
has been modified or any of its dependents are out of date. Obviously this process may recurse.
