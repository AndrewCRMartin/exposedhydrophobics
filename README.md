Exposed Hydrophobicity
======================

exposedhphob.pl V1.0.1 (c) 2020 UCL, Prof. Andrew C.R. Martin
-------------------------------------------------------------

```
Usage: exposedhbob.pl [-hphob=hphobfile] startres stopres file.pdb
       -hphob   - specify hydrophobicity file [/home/amartin/data/consensus.hpb]
       startres - first residue ID in the format [c[.]]nnn[i]
       stopres  - last residue ID in the format [c[.]]nnn[i]
       file.pdb - PDB file
```

Outputs a 'quality' score (0-1) for each residue in the specified range.

The program expects that `bioptools` is installed and in the path and
that the `DATADIR` environment variable has been set to point to the
BiopTools/BiopLib data directory.

It calculates the relative residue solvent accessibility (in the range
0 to 1) for the provided PDB file. For each residue in the specified
range, it obtains the Eisenberg consensus hydrophobicity values for
each residue. These are normalized about the zero point such that they
run from -1 to +1 (i.e. the negative and positive values are
normalized separately). A quality score is the calculated by combining
the accessibility and and hydrophobicity scores.

The quality score is calculated as:

```
      /  1 + (H * (1-A))   if (H<0)
  Q = |
      \  1 - (H * A)       otherwise
```

where *A* = accessibility (0..1) and *H* = hdrophobicity (-1..+1)

The total and average scores are also output.

The calculation favours buried hydrophobics and exposed hydrophilics;
it penalizes exposed hydrophobics and buried hydrophilics.

