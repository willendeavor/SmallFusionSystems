# SmallFusionSystems
A package that implements a database similar to the SmallGroups one, made to be compatible with the FusionSystems package by Parker + Semeraro. Note the latest version of that package (https://github.com/chris1961parker/Fusion-Systems) is included here so this is self-contained.

This is not the latest version but rather a stable separate release, the latest version will be part of the overall fusion systems package I have been working on. Updates to the database will be occasionally incorporated and compatibility between the two should be easy to maintain. 

## Usage
Open MAGMA from the package root directory and run AttachSpec("spec"); To be able to run it from elsewhere you will have to update the file paths throughout the code, currently it assumes MAGMA has been launched from the root directory and therefore all references are based off that. At some point I will improve this but I have to yet to incorporate a satisfactory workaround. Likewise this package makes use of the OS commands in order to create directories or list files so I suspect that will cause issues in different environments.

## Overview
For a given fusion system `F` all necessary information required to construct the fusion system can be saved in a file `filename` via `WriteFusionRecord(filename, F)`. This creates a file which can be loaded by `R := LoadFusionSystemRecord(filename)`, this returns not a fusion system but instead a record of the format `FusionRecord`. The idea is that we can access some pertinent information about `F`, such as the number of essential subgroups, the underlying $p$-group etc. without having to actually construct it. Creating the fusion system is then done by calling `LoadFusionSystem(R)`.

Included in this package is many fusion systems which have already been calculated and akin to the SmallGroups package these can be loaded as wanted. The fusion systems are grouped according to the order of the underlying $p$-group so that for example fusion systems over a group of order $3^5$ are all kept in `data/SmallFusionSystems/p_3/n_5`, each file `FS_i` in this directory then corresponds to a fusion system.

To load this fusion system we simply execute `SmallFusionSystem(3^5, i)`. If you want to find fusion systems based upon the isomorphism type of $S$ there is also functionality for this, `NumberSmallFusionSystems(S)` returns a list of the indices which correspond to fusion systems over $S$. The function `AllSmallFusionSystems(S)` will return a list of the actual fusion systems.

## Notes
All the fusion systems included were converted from those found in https://github.com/chris1961parker/Fusion-Systems as such it is possible there are some missing since `AllFusionSystems` runs assuming the fusion systems have trivial core and are $p$-perfect. It is possible to add a fusion system to the database via `AddSmallFusionSystem`, this relies on using `IsIsomorphic` to determine if the fusion system is already present.


I have not done any extensive testing but initial observations seem to suggest that the loading of fusion systems in this package is faster than that of the FusionSystems package. For example running load "All3to6", which doing so returns a list of all fusion systems over groups of order $3^6$ took approx 150 seconds while `AllSmallFusionSystems(3^6)` took 75 seconds. Of course saving is however fairly slow, adding all these fusion systems took 34 minutes.
