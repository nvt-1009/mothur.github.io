---
title: 'make.clr'
tags: 'commands'
redirect_from: '/wiki/Make.clr.html'
---
The **make.clr** command converts a [ shared](/wiki/Shared_file) file
to a [ centered log ratio](/wiki/Clr_file) file. The make.clr
command parameters are shared, groups, zero and label. The shared file
is required.

## Default Settings

The shared file is required.

    mothur > make.clr(shared=final.opti_mcc.shared)

The clr file will look like:

    label  Group   numOtus Otu001  Otu002  Otu003  Otu004  Otu005  Otu006  ...
    0.03   F3D0    477 9.88996 9.18445 9.54911 9.5817  10.2308 9.40279 ...
    0.03   F3D1    477 9.60907 9.43451 8.71598 7.15374 7.34357 8.02411 ... 
    0.03   F3D141  477 9.95792 9.74602 9.59162 10.2709 10.0893 9.48213 ...
    0.03   F3D142  477 9.63123 9.71172 8.85024 8.94842 9.68349 9.2929 ...
    0.03   F3D143  477 9.31475 9.00044 9.18714 9.446   10.0193 9.26821 ...
    0.03   F3D144  477 9.94975 9.43993 9.53749 9.8189  10.3886 9.65467 ...
    0.03   F3D145  477 10.3498 10.0028 10.0537 10.2468 10.5823 10.084...
    0.03   F3D146  477 9.2422  8.83781 8.97917 9.67714 9.79838 9.17101 ...
    0.03   F3D147  477 10.8948 10.6442 10.2095 10.5707 11.1926 10.5693 ...
    0.03   F3D148  477 10.2892 10.1178 9.76077 10.4354 11.0028 10.24023 ...
    0.03   F3D149  477 10.2242 10.0888 9.97982 10.3854 10.4152 9.98204 ...
    0.03   F3D150  477 9.21106 8.8547  9.58328 9.9294  9.29564 9.26974 ...
    0.03   F3D2    477 12.0676 10.9716 10.5374 9.29773 7.6902  9.16022 ...
    0.03   F3D3    477 11.341  10.7271 10.2862 9.18923 6.16589 9.3770 ...
    0.03   F3D5    477 9.49838 9.25596 9.26208 8.58889 5.70137 8.47747 ...
    0.03   F3D6    477 10.8964 10.3273 10.0652 9.65305 4.66436 9.55513 ...
    0.03   F3D7    477 10.8735 10.5142 10.2923 9.90326 4.87351 9.5801 ...
    0.03   F3D8    477 9.02401 9.41283 9.34594 8.14137 2.14137 8.58432 ...
    0.03   F3D9    477 9.71762 9.49965 9.69759 8.51499 3.27468 8.94711 ...

## Options

### groups

The groups parameter allows you to specify which of the groups in your
sharedfile you would like included. The group names are separated by
dashes.

    mothur > make.clr(shared=final.opti_mcc.shared, groups=F3D7-F3D8-F3D9)

### label

The label parameter allows you to select what distance levels you would
like, and are also separated by dashes.

    mothur > make.clr(shared=final.opti_mcc.shared, label=0.03)

### zero

The zero parameter allows you to set an value for zero OTUs. Default is

0\.1.

    mothur > make.clr(shared=final.opti_mcc.shared, zero=0.01)

## Revisions

-   1.44.0 - First Introduced.
    [\#695](https://github.com/mothur/mothur/issues/695)


