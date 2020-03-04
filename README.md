==========================================================================
README
==========================================================================
Author : Christopher Torng
Date   : June 7, 2019

This is a 45nm ASIC design kit for mflowgen, a modular ASIC/FPGA flow
generator:

- https://github.com/cornell-brg/mflowgen

This kit uses FreePDK45 and the NanGate Open Cell Library.

- FreePDK45: https://www.eda.ncsu.edu/wiki/FreePDK45:Contents
- NanGate: https://projects.si2.org/openeda.si2.org/help/group_ld.php?group=63}

The FreePDK45 kit is an open-source generic process design kit (PDK)
(i.e., does not correspond to any real process and cannot be fabricated)
that allows researchers and students to experiment with designing in a
modern technology node without signing restrictive non-disclosure
agreements or paying for licenses. The PDK allows you to use commercial
full-custom layout tools (e.g., Cadence Virtuoso) to design both analog
and digital circuits.

The Nangate Open Cell Library is a generic open-source digital
standard-cell library designed using the FreePDK45 kit.

This package was assembled from these kits to be used as an ASIC design
kit for designs built with mflowgen. See more information about mflowgen
at its github repo.

--------------------------------------------------------------------------
Modifications -- 03/04/2020
--------------------------------------------------------------------------

Change:

- rtk-tech.lef: One-line change to set MANUFACTURINGGRID to 0.0025 instead
  of 0.0050

OpenRAM is an open-source memory compiler:

- https://openram.soe.ucsc.edu/

To interact nicely with OpenRAM, we modified the routing technology LEF
(i.e., rtk-tech.lef) such that "MANUFACTURINGGRID" is "0.0025" instead of
"0.0050" (a one line change). Otherwise Cadence Innovus complains that the
SRAM LEF has pins that are not on the manufacturing grid.

Since this is a fake technology, we think this is okay.

--------------------------------------------------------------------------
Modifications -- 12/17/2019
--------------------------------------------------------------------------

Change:

- calibre-lvs.rule: One-line change to set precision to 10000 instead of
  2000

In order to run LVS, the precisions have to match between the LVS rule
file precision and the GDS database precision. Otherwise Calibre says
this:

    ERROR: Rule file precision 2000 is not consistent with database
    precision 10000 in input file design_merged.gds

The stdcells.gds has a precision of 10000. For example, here is a message
printed from calibredrv when reading the gds for the minimum size
inverter:

    % calibredrv -a layout filemerge -in stdcells.gds -topcell INV_X1
                 -out dummy.gds

    Output file precision will be 10000, based on the lowest common
    multiple of the input file precision(s).

To run LVS successfully, our solution is just to make the LVS rule deck
expect a precision of 10000.

--------------------------------------------------------------------------
Modifications -- 06/07/2019
--------------------------------------------------------------------------

Initial commit

Base set of files from FreePDK45 and NanGate Open Cell Library assembled
into an ASIC design kit (ADK) for use with mflowgen

