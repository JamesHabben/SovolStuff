# Updating Timezone Information on Sovol SV06+ with Sovol Klipper Screen

This guide provides instructions on how to update the timezone settings on your Sovol SV06+ 3D printer equipped with a Sovol Klipper screen. The original code had limited timezone options, and this update expands those options to include a broader range of timezones.

This will probably work on other Sovol models as well, but I only have an SV06+ to test with. If you update a different model, please submit an issue here to let me know and I can update this documentation.

If you find any issue with timezone names, offsets, values, or something missing, please submit an issue here to let me know and I can update the code.

## Prerequisites
- SSH access to the Sovol SV06+ Klipper.
- Ensure you have a backup of your original `zone.py` file (explained below).

## Instructions

1. **SSH into your Sovol Klipper Screen**
   - Use an SSH client to connect to your printer. You will need the IP address and credentials for access. Here is an example of how to SSH into your printer:
     ```bash
     ssh mks@<IP_ADDRESS_OF_PRINTER>
     ```
   - When prompted for a password, use `makerbase`.

2. **Navigate to the timezone script directory**
   - Once logged in, navigate to the directory containing the `zone.py` file. Typically, this can be done with:
     ```bash
     cd KlipperScreen/panels/
     ```

3. **Verify the current `zone.py` file**
   - Before making any changes, ensure that your `zone.py` file matches the my backed up version. You can get the hash of your current file:
     ```bash
     sha256sum zone.py
     ```
     Compare with my backup file hash: `ebf114783ca478465619a67b7d93b8ad03dd192311629606aaa0400b158b4ee0`

4. **Rename the existing `zone.py` to `zone.py.bak`**
   - It's important to keep a backup of the original configuration:
     ```bash
     mv zone.py zone.py.bak
     ```

5. **Download the updated `zone.py` from GitHub**
   - Pull the updated `zone.py` file from this GitHub repository:
     ```bash
     wget https://github.com/JamesHabben/SovolStuff/raw/main/timezone/zone.py
     ```

6. **Restart the KlipperScreen service**
   - After updating the `zone.py` file, you need to restart the KlipperScreen service to apply the changes. This might prompt you for the 'makerbase' password. Run the following command:
     ```bash
     sudo systemctl restart KlipperScreen
     ```
   - Verify that the new timezone settings are available and functioning as expected.

## Troubleshooting
If you encounter issues, you can revert to the original settings by renaming `zone.py.bak` back to `zone.py` and restarting the printer.

For any questions or further assistance, please refer to the Sovol community forums or the documentation provided with your Sovol SV06+.