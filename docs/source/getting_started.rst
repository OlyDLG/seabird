****************************
Getting Started with Seabird 
****************************

Inside python
=============

    >>> import seabird



In a python script, one can use like this::

    >>> from seabird.cnv import fCNV
    >>> profile = fCNV('your_file.cnv')
    >>> profile.attributes  # It will return the header, as a dictionary.
    >>> profile.keys() # It will list the available variables.
    >>> profile['temperature2'] # If temperature2 was on the .keys(), this is how you get the data. It will be a masked array.

The data from a profile is hence treated as it was a dictionary of Masked Arrays. To plot it, one could::

    >>> import matplotlib.pyplot as plt
    >>> plt.plot(profile['depth'], profile['temperature'], '.')
    >>> plt.show()

From the terminal
=================

One way to use is running on the shell the cnvdump. 
Independent of the historical version of the cnv file, it will return a default structure::

    cnvdump your_file.cnv

That can be used in a regular shell script. 
For example, let's consider a directory cruise1 with several sub directories, one for each leg of the cruise. 
One could list all the latitudes of each CTD cast like::

    for file in `find ./cruise1 -iname '*.cnv'`
    do cnvdump $file | grep latitude
    done

To convert a .cnv to a standard NetCDF, run::

    cnv2nc your_file.cnv