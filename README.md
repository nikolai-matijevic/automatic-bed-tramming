This is a proof of concept for the BLV MGN Cube and a CR10 style bed.

Essentially I replaced the wheels with NEMA 17 stepper motors which are mounted with a printed part and control the height of the point using a special printed coupler as well as a brass insert. It would also be possible to customize the part to use a nut instead.

If you want to try that setup out on your own printer you can either use the STL files if you have the same printer and bed or adjust the step files for your own.

# Configuration

Your `printer.cfg` needs to include the following configuration to load the module:

```properties
[auto_bed_tramming]
screw_thread: CW-M3

screw1: X,Y
screw1_stepper: stepper_name1

screw2: X,Y
screw1_stepper: stepper_name2

screw3: X,Y
screw3_stepper: stepper_name3

...
```

At least 3 points are needed to adjust the bed tilt. Add additional screws/motors as needed. To pair the motors to the screws you also have to add their name to the right screw.

You will also have to have a probe configured in the `printer.cfg`.

The M3 screws I'm using for tramming the bed have a pitch of 0.5 mm which simply translates to a rotation distance of 0.5 in the config file for each of the stepper motors.

# Usage

Calling `AUTO_BED_TRAMMING` will probe the configured points on the bed, calculate the difference in height between the screws and adjust them to the height of one of the screws.

## Direction

You can also specify the optional `DIRECTION` parameter which can either be `CW` or `CCW` depending on the direction which should be enforced. This is especially useful right after adding the motors or if they are bottoming out. Subsequent adjustments should not need the `DIRECTION` parameter as they should only be small and not hit the upper or lower limit.

## Maximum Delta

The `MAX_DELTA` parameter specifies the maximum differnce between the probed points. If they exceed this value the module will throw an error.

## Retries

Using `RETRIES` also requires `MAX_DELTA` and tries to adjust the screws until the probed points are within the `MAX_DELTA` value or exceed the amount of `RETRIES`.

# Contact

Usually I would able to answer questions on the BLV Discord server but since my account has been disabled and the support team seems to have no interest in answering my emails I set up a new account (nima#8307). I am unable to join the server using this new account which means that I can't reply to messages using this one or my original account.

You can either contact me through Discord or GitHub. If you have any questions or need help setting up automatic bed tramming on your printer I'll be happy to answer and give assistance.

![mounted assembly](https://github.com/nikolai-matijevic/automatic-bed-tramming/blob/master/Resources/IMG_20220206_083627.jpg?raw=true)
