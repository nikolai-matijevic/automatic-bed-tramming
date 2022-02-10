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

# Usage

After running `G28` and `SCREWS_TILT_CALCULATE` you will get an output similar to this:
```
01:20 means 1 full turn and 20 minutes, CW=clockwise, CCW=counter-clockwise
Lower Left (base) : x=68.5, y=40.0, z=2.40900
Upper Right : x=308.5, y=280.0, z=2.41150 : adjust CCW 00:00
Upper Left : x=68.5, y=280.0, z=2.40775 : adjust CW 00:00
Lower Right : x=308.5, y=40.0, z=2.40650 : adjust CW 00:00
```

Now you can adjust the screws by calling the `ADJUST_SCREWS` macro with the values from the output above:
```
ADJUST_SCREWS BASE=2.40900 UR=2.41150 UL=2.40775 LR=2.40650
```

Do this until `SCREWS_TILT_CALCULATE MAX_DEVIATION=0.01` doesn't output `!! bed level exceeds configured limits (0.01mm)! Adjust screws and restart print.` anymore but remember to home the Z axis before that each time.

I would advise adding a `G28` as well as `SCREWS_TILT_CALCULATE MAX_DEVIATION=0.01` to the end of the macro to automate the process until the desired result is reached.

# What's next?

I am working on further automating the process by having Klipper loop over the commands and adjusting the stepper motor positions by itself. This way you could just add a macro call to always have a perfectly trammed bed before each print.

![mounted assembly](https://github.com/nikolai-matijevic/automatic-bed-tramming/blob/master/Resources/IMG_20220206_083627.jpg?raw=true)