# Sovol Klipper Screen Package Version Analysis

This document outlines the process and findings from analyzing the versions of various packages used in Sovol's Klipper screen setup. The goal is to identify any custom modifications made specifically for Sovol printers and to assess the feasibility of updating or installing newer versions of each package without issues.

## Background

Sovol's Klipper screen setup includes several key software components. To ensure compatibility and stability, it's crucial to understand the versions and modifications of these packages compared to their original sources.

## Package Version Comparison

The following table summarizes the current analysis of the package versions used in Sovol's setup compared to their respective sources:

| Package       | Sovol Version | Source Version | Source Date | Source URL | Notes |
|---------------|---------------|----------------|-------------|------------|-------|
| Crowsnest     | Customized    | 20ed6a8b58     | 2023-04-15 | [Crowsnest 20ed6a8b58](https://github.com/mainsail-crew/crowsnest/tree/20ed6a8b585a92e8a0e7d8333e81b6e8ca7044e1) | Custom RTSP server setup and ustreamer binary. See `diff-crowsnest.txt` |
| Fluidd        | Exact Match   | v1.23.2        | 2023-02-20  | [Fluidd v1.23.2](https://github.com/fluidd-core/fluidd/releases/tag/v1.23.2) | Direct copy of the release |
| Kiauh         | Exact Match   | 7989cec8d | 2023-09-01 | [Kiauh 7989cec](https://github.com/dw-0/kiauh/tree/7989cec8d4e99cc31cac5e24753c8690f16bcde8) | Direct copy of the code at this commit |
| Klipper       | Minor difference | Post-0.11.0   | 2023-02-13  | [Klipper e6ef48c](https://github.com/Klipper3d/klipper/tree/e6ef48cdf7b7e23f422cbe0ec46091001b840674) | See `diff-klipper.txt` |
| [KlipperScreen](KlipperScreen.md) | TBD           | TBD            |   TBD          | TBD        | Looks to be somewhere around 2023-05-07   |
| Mainsail      | Exact Match   | v2.6.0         | 2023-06-19  | [Mainsail v2.6.0](https://github.com/mainsail-crew/mainsail/releases/tag/v2.6.0) | Direct copy of the compiled release |
| Moonraker     | Minor differences | c8767dadd     | 2023-02-27  | [Moonraker c8767dadd](https://github.com/Arksine/moonraker/tree/c8767daddf6d5930841a8279767aaf20362c5eb0) | See `diff-moonraker.txt` |

## Methodology

1. **Identify the installed version on Sovol's Klipper screen**: Check the version information from the system or package manifests.
2. **Compare with the source repository**: Use tools like `diff` to compare the Sovol version against the specific commit or release in the source repository.
3. **Document differences**: Any differences, especially in configuration or patches specific to Sovol, are noted.

## Findings

- **Crowsnest**: The Sovol version includes specific configurations and additional binaries for RTSP streaming and ustreamer, which are not present in the source commit. These modifications may be critical for specific functionalities in Sovol's setup.
- **Fluidd**: The Sovol version of Fluidd is an exact copy of the release v1.23.2, ensuring full compatibility with the official release and simplifies updates.
- **Kiauh**: The Sovol version of Kiauh is an exact copy of the code at commit `7989cec8d`, ensuring that all functionalities are preserved as per the original repository.
- **Klipper**: The Sovol version of Klipper aligns with a commit several after the official 0.11.0 release, specifically commit `e6ef48c`. The diff analysis shows no significant custom modifications, indicating good compatibility with this version. One notable file is `klippy/extras/gcode_shell_command.py` that does not exist anywhere in the `klipper` repo, but does exist in the `kiauh` repo.
- **Mainsail**: The Sovol version of Mainsail is a direct copy of the compiled release v2.6.0, with no modifications. This ensures full compatibility with the official release and simplifies updates.
- **Moonraker**: The analysis shows that the Sovol version of Moonraker is closely aligned with the commit `c8767dadd` from the official Moonraker repository. The differences are minimal, suggesting that updates to newer versions may be feasible with little to no modifications.

## Next Steps

- **Complete the analysis for other packages**: The versions and modifications for KlipperScreen need to be analyzed similarly.
- **Testing updates**: Any potential updates based on the findings should be tested in a controlled environment to ensure compatibility with Sovol's hardware and software setup.

## Conclusion

This ongoing analysis is crucial for maintaining and potentially enhancing the functionality of Sovol's Klipper screen setup. By understanding the specifics of the installed packages, we can make informed decisions about updates and modifications.
