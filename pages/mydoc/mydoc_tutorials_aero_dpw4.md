---
title: DPW4 aircraft
keywords: tutorial, dpw4
summary: 
sidebar: mydoc_sidebar
permalink: mydoc_tutorials_aero_dpw4.html
folder: mydoc
---

{% include note.html content="We recommend going through the tutorial in [Get started](mydoc_get_started_download_docker.html) before running this case." %}

The following is an aerodynamic shape optimization case for an aircraft wing-body-tail configuration at transonic conditions. The summary of the case is as follows:

<pre>
Case: Aircraft aerodynamic optimization
Geometry: CRM wing, body, and tail
Objective function: Drag coefficient
Design variables: 216 FFD points moving in the z direction, 9 wing twists, one tail rotation, one angle of attack
Constraints: Volume, thickness, LE/TE, and lift constraints (total number: 771)
Mach number: 0.85
Reynolds number: 5 million
Mesh cells: 100K
Adjoint solver: DARhoSimpleCFoam
</pre>

To run this case, first download [tutorials](https://github.com/DAFoam/tutorials/archive/master.tar.gz) and untar it. Then go to tutorials-master/DPW4_Aircraft and run this command to start the DAFoam docker container.

<pre>
docker run -it --rm -u dafoamuser --mount "type=bind,src=$(pwd),target=/home/dafoamuser/mount" -w /home/dafoamuser/mount dafoam/opt-packages:{{ site.latest_version }} bash
</pre>

**Now you are on the DAFoam Docker container**, run the "preProcessing.sh" script to generate the mesh:

<pre>
./preProcessing.sh
</pre>

Then, use the following command to run the optimization with 16 CPU cores:

<pre>
mpirun -np 16 python runScript.py 2>&1 | tee logOpt.txt
</pre>


{% include links.html %}