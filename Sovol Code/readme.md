# Sovol Klipper Screen Package Version Analysis

This document outlines the process and findings from analyzing the versions of various packages used in Sovol's Klipper screen setup. The goal is to identify any custom modifications made specifically for Sovol printers and to assess the feasibility of updating or installing newer versions of each package without issues.

## Background

Sovol's Klipper screen setup includes several key software components. To ensure compatibility and stability, it's crucial to understand the versions and modifications of these packages compared to their original sources.

## Package Version Comparison

The following table summarizes the current analysis of the package versions used in Sovol's setup compared to their respective sources:

| Package       | Sovol Version | Source Version | Source Date | Source URL | Notes |
|---------------|---------------|----------------|-------------|------------|-------|
| Moonraker     | Minor differences | c8767dadd     | 2023-02-27  | [Moonraker c8767dadd](https://github.com/Arksine/moonraker/tree/c8767daddf6d5930841a8279767aaf20362c5eb0) | See `diff-moonraker.txt` |
| KlipperScreen | TBD           | TBD            |             | TBD        | TBD   |
| Klipper       | Minor difference | Post-0.11.0   | 2023-02-13  | [Klipper e6ef48c](https://github.com/Klipper3d/klipper/tree/e6ef48cdf7b7e23f422cbe0ec46091001b840674) | See `diff-klipper.txt` |
| Mainsail      | Exact Match       | v2.6.0         | 2023-06-19  | [Mainsail v2.6.0](https://github.com/mainsail-crew/mainsail/releases/tag/v2.6.0) | Direct copy of the compiled release  |
| Fluidd        | TBD           | TBD            |             | TBD        | TBD   |

## Methodology

1. **Identify the installed version on Sovol's Klipper screen**: Check the version information from the system or package manifests.
2. **Compare with the source repository**: Use tools like `git diff` to compare the Sovol version against the specific commit or release in the source repository.
3. **Document differences**: Any differences, especially in configuration or patches specific to Sovol, are noted.

## Findings

- **Moonraker**: The analysis shows that the Sovol version of Moonraker is closely aligned with the commit `c8767dadd` from the official Moonraker repository. The differences are minimal, suggesting that updates to newer versions may be feasible with little to no modifications.
- **Klipper**: The Sovol version of Klipper aligns with a commit several after the official 0.11.0 release, specifically commit `e6ef48c`. The diff analysis shows no significant custom modifications, indicating good compatibility with this version. One notable file is `klippy/extras: gcode_shell_command.py` that does not exist anywhere in the `klipper` repo, but does exist in the `kiauh` repo.
- **Mainsail**: The Sovol version of Mainsail is a direct copy of the compiled release v2.6.0, with no modifications. This ensures full compatibility with the official release and simplifies updates.

## Next Steps

- **Complete the analysis for other packages**: The versions and modifications for KlipperScreen and Fluidd need to be analyzed similarly.
- **Testing updates**: Any potential updates based on the findings should be tested in a controlled environment to ensure compatibility with Sovol's hardware and software setup.

## Conclusion

This ongoing analysis is crucial for maintaining and potentially enhancing the functionality of Sovol's Klipper screen setup. By understanding the specifics of the installed packages, we can make informed decisions about updates and modifications.
