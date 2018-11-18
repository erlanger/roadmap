# SWI-Prolog Roadmap

This (otherwise) empty repository is intended to discuss future development around SWI-Prolog.
If you would like to see **larger** issues around the project changed or added, please raise an
issue on this repository.  Please do **not** use this for reporting **bugs**.  To report bugs, use
the [issues repository](https://github.com/SWI-Prolog/issues) or, if you can associate the
bug with a specific source repository, the issue repository of that repository.  Example topics for
the roadmap are

  - New core features (e.g., _tabling_, performance enhancements, scalability)
  - Desired (new) libraries
  - Serious changes to libraries (e.g., change the representation of literals in the RDF libraries)
  - Website redesign
  - Package infrastructure
  - Tutorials
  - Development environment (local, [SWISH](http://swish.swi-prolog.org))

## Saved state portability
Following a discussion about a port to Android (in SWI-Prolog/swipl-devel#358), there was a concern about creating saved states on one platform and moving them to another platform, especially from a native platform to a different platform (like android). Two cases were observed:
1. Saved state does not use foreign libraries (e.g. only prolog code)
    - In this case the saved state will work on any other platform with the same pointer size
      (e.g. 32-bit or 64-bit)
    - We can then embed pointer size information in the saved state, and use this saved state
       on the target platform _if the pointer size matches_.
2. Saved state  depends on foreign (.so) libraries using `--foregin=save` option
    - In this case, the saved sate depends not only on the **pointer size**, but also on the
      **architecture** and the **operating system** being used.
    - We can embed architecture information in the saved state, and decide --_at runtime_--
       if the target architecture is compatible with the one embedded in the saved state. This
       will be a best effort approach.
