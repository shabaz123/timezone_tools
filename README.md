Timezone Tools
==============

Timezone encoded with colors : For very approximate timezone offset determination
---------------------------------------------------------------------------------
Timezone rules are complicated. The timezone_color_encoded.png file contains a 1080x540 resolution image (3x3 pixels representing one degree longitude and latitude). It is _not_ highly accurate, but it will provide a good first guess at the timezone offset. For most populated areas, I think the file may be reasonably accurate for a large percentage of people in populated areas, unless you live fairly close (well, perhaps 50 km) to a timezone boundary, or if you are in a location with more unusual-than-normal timezone rules.

The timezone.png file is deliberately fairly low-resolution, so that it can be used in embedded applications (either directly, or with some sort of post-processing).

Each pixel has the following encoding, where the pixel color is (redval, greenval, blueval) and each value is 0-255

The red channel encodes the integer value of the timezone offset:

```
tz = ((int)(redval >> 3)) - 15;
```

The tz value will be between -14 and +14.

The green channel encodes a modifier:

```
if (greenval == 0)
    modifier = 0;
else
    modifier = ((int)(greenval >> 4)) - 4;
```

The modifier is an integer number between -3 and +3, representing -45, -30, -15, 0, +15, +30, +45 minutes

You could convert the modifier to a float and divide by 4, to get a fractional value of an hour if desired (i.e. -0.75 to +0.75).

The blue channel does not encode anything (ignore the contents of the blue channel).

