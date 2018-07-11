# para-std

Paragliding Standards and Proposals

![Paragliding pilot enjoying an evening flight](https://raw.githubusercontent.com/Kadrian/para-std/master/nicolas-tissot-435976-unsplash.jpg)
<sup>Photo by Nicolas Tissot on Unsplash</sup>

## Paraglider Standard Attributes

A paraglider wing can be described by a number of attributes.

Different manufacturers use different attribute names. For example `Takeoff weight` and `Weight in flight` are the same, just called differently. That's what makes it hard for pilots to compare paragliders.

To build [gliderbase.com](https://gliderbase.com) required describing a paraglider in a comparable, machine-readable format.

I'm proposing a standard way of describing a paraglider in a JSON format.

**To manufacturers**: Feel free to use this format for new models. Feel free to comment and contribute.

## Paraglider Format

### Simple Example

A wing called **Wing 123** by the manufactuerer **Great Wings Inc.**, which is available in one size:
**S**.
That size was certified as **LTF/EN-A**, the area is **24 m2**, The **certified takeoff weight** ranges from **90 kg** to **120 kg**.
Also, a **trimmer** system is available.

```javascript
{
  "name": "Wing 123",
  "manufacturer": {
    "name": "Great Wings Inc."
  },
  "sizes": [
    {
      "name": "S",
      "attributes": [
        {
          "name": "CERTIFICATION",
          "value": "LTF/EN-A"
        },
        {
          "name": "AREA_FLAT",
          "value": "24",
          "unit": "m2"
        },
        {
          "name": "TAKEOFF_WEIGHT",
          "unit": "kg",
          "value": {
            "from": "90",
            "to": "120"
          },
          "additionalInfo": "certified"
        },
        {
          "name": "HAS_TRIMMER",
          "value": true
        }
        // MORE ATTRIBUTES
        // {
        //   "name": ...,
        //   "value": ...,
        //    ...
        // }
      ]
    }
    // MORE SIZES
    // {
    //   "name": "M",
    //   "attributes": [...],
    //    ...
    // }
  ]
}
```

### Possible attribute names

Here's a proposal for possible paraglider attribute names that can be interesting to pilots.
This covers most of what a paraglider manufacturer specifies for a new wing.

Right now, these attributes mostly concern:

* Paraglider geometry
* Paraglider flight characteristics
* Paraglider safety

Especially, paraglider materials are _not_ covered yet. Contributions are always welcome!

**Very common**

| Usual type | Name                   | English description    |
| ---------- | ---------------------- | ---------------------- |
| NUMBER     | TAKEOFF_WEIGHT         | Takeoff weight         |
| NUMBER     | GLIDER_WEIGHT          | Glider weight          |
| NUMBER     | CELLS                  | Cells                  |
| NUMBER     | AREA_FLAT              | Flat area              |
| NUMBER     | AREA_PROJECTED         | Projected area         |
| NUMBER     | SPAN_FLAT              | Flat span              |
| NUMBER     | SPAN_PROJECTED         | Projected span         |
| NUMBER     | ASPECT_RATIO_FLAT      | Flat aspect ratio      |
| NUMBER     | ASPECT_RATIO_PROJECTED | Projected aspect ratio |
| NUMBER     | LINE_DIAMETERS         | Line diameters         |
| NUMBER     | TOTAL_LINE_LENGTH      | Total line length      |
| NUMBER     | CHORD                  | Chord                  |
| STRING     | CERTIFICATION          | Certification          |

**Less common, but used across manufacturers**

| Usual type | Name                        | English description          |
| ---------- | --------------------------- | ---------------------------- |
| NUMBER     | SPEED_TRIM                  | Trim speed                   |
| NUMBER     | SPEED_MAX                   | Max. speed                   |
| NUMBER     | MAX_TRAVEL_TRIMMER          | Max. trimmer travel          |
| NUMBER     | MAX_TRAVEL_ACC              | Max. accelerator travel      |
| BOOL       | HAS_ACC_SYSTEM              | Has accelerator system       |
| NUMBER     | TRIMMER_LENGTH              | Trimmer length               |
| NUMBER     | TOTAL_LINES                 | Total lines                  |
| NUMBER     | RISERS_LENGTH               | Risers length                |
| NUMBER     | BRIDLE_HEIGHT               | Distance to risers           |
| STRING     | RISERS                      | Risers                       |
| NUMBER     | MAX_LINE_LENGTH_WITH_RISERS | Max. line length with risers |

**Rare, used by individual manufacturers, sometimes controversial**

| Usual type | Name                             | English description                  |
| ---------- | -------------------------------- | ------------------------------------ |
| NUMBER     | BEST_GLIDE                       | Best glide                           |
| NUMBER     | MIN_SINK_RATE                    | Min. sink rate                       |
| STRING     | NUMBER_MAIN_LINES                | Number of main lines                 |
| STRING     | MINI_WING_CHARACTER              | Mini Wing Character                  |
| BOOL       | HAS_TRIMMER                      | Has trimmer                          |
| NUMBER     | SEATS                            | Seats                                |
| BOOL       | SHOCK_AND_LOAD_TEST              | Shock and load test                  |
| STRING     | CERTIFICATION_NUMBER             | Certification number                 |
| STRING     | CERTIFICATION_PROCEDURES         | Certification procedures             |
| BOOL       | CERTIFICATION_FOLDING_LINES_USED | Folding lines used for certification |
| NUMBER     | LINEAR_SCALING_FACTOR            | Linear scaling factor                |
| NUMBER     | LINE_LENGTH                      | Line length                          |

### The attribute format

**Principles**

* There are three different kinds of attributes
  * Number attributes: Often have a unit like _m_, _mm_, _kg_. May be a number range too. Can have a number variance (+/-).
  * Bool attributes: Yes / No
  * String attributes: For attributes like `CERTIFICATON`: `LTF/EN-B`.
* All attribute values are optional (different paraglider sizes may not have one or the other attribute)
* All attributes have an optional `additionalInfo` to provide more details like `extended` / `certified` / `only when accelerating`.

**Technical definition**

Using a type system called [Flow](https://flow.org/en/), we can describe the different attribute types.

```javascript
// @flow

type AttributeType = StringAttributeType | NumberAttributeType | BoolAttributeType;

type StringAttributeType = {
  name: string,
  value: ?string,
  additionalInfo?: string,
};

type BoolAttributeType = {
  name: string,
  value: ?boolean,
  additionalInfo?: string,
};

type NumberAttributeType = {
  name: string,
  value: ?(number | RangeType),
  valueVariance?: number,
  unit?: string, // If no unit, then it's probably a "count"
  additionalInfo?: string,
};

type RangeType = {
  from: number,
  to: number,
};
```
