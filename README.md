# automatic-bed-tramming
Replace manual knobs with motors for more accurate bed tramming

This is a proof of concept for the BLV MGN Cube and a CR10 style bed.

Essentially I replaced the knobs with NEMA 17 stepper motors which are mounted with a printed part and control the height of the corner using a special printed coupler as well as a brass insert.

If you want to try that setup out on your own printer you can either use the STL files if you have the same printer and bed or adjust the step files for your own.

To use the macro effectively you have to add and customize the following lines in your `printer.cfg`:

```properties
[screws_tilt_adjust]
screw1: 68.48,40
screw1_name: Lower Left
screw2: 308.48,280
screw2_name: Upper Right
screw3: 68.48,280
screw3_name: Upper Left
screw4: 308.48,40
screw4_name: Lower Right
horizontal_move_z: 10
screw_thread: CW-M3
```

![mounted assembly](https://github.com/nikolai-matijevic/automatic-bed-tramming/blob/master/Resources/IMG_20220206_083627.jpg?raw=true)