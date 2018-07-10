# para-std

Paragliding Standards and Proposals

# Paraglider Standard Attributes

A paraglider can be described by a number of attributes. So far, different manufacturers use different attribute names.

For example `Takeoff Weight` and `Weight in flight` are the same, just called differently.

That's what makes it hard for pilots to compare paragliders.
That also means paraglider products are not easy to work with for computers.

I'm proposing a standard way of describing a paraglider in a JSON format.

## Paraglider Format

### Simple Example

A wing called **Wing 123** by the manufactuerer **Great Wings Inc.**, which is available in one Size:
**S**.
For that size, the area is **24 m2**, The **certified takeoff weight** ranges from **90 kg** to **120 kg**.
Also, a **trimmer** system is available.

```json
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
          "name": "FLAT_AREA",
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

### All possible attribute names

Here's a proposal for possible paraglider attribute names. This covers most of what a paraglider manufacturer specifies for a new wing.

**This is far from perfect**

Please feel free to contribute when you see something missing or inconsistent.

```
| Usual type | Name | English description |
| NUMBER | AREA_FLAT | Flat area |
| NUMBER | AREA_PROJECTED | Projected area |
| NUMBER | TAKEOFF_WEIGHT | Takeoff weight |
| NUMBER | GLIDER_WEIGHT | Glider weight |
| NUMBER | SPAN_FLAT | Flat span |
| NUMBER | SPAN_PROJECTED | Projected span |
| NUMBER | ASPECT_RATIO_FLAT | Flat aspect ratio |
| NUMBER | ASPECT_RATIO_PROJECTED | Projected aspect ratio |
| NUMBER | CELLS | Cells |
| STRING | RISERS | Risers |
| NUMBER | SPEED_TRIM | Trim speed |
| NUMBER | SPEED_MAX | Max. speed |
| STRING | CERTIFICATION | Certification |
| NUMBER | MAX_TRAVEL_TRIMMER | Max. trimmer travel |
| NUMBER | MAX_TRAVEL_ACC | Max. accelerator travel |
| BOOL | HAS_ACC_SYSTEM | Has accelerator system |
| BOOL | HAS_TRIMMER | Has trimmer |
| NUMBER | CHORD | Chord |
| NUMBER | TRIMMER_LENGTH | Trimmer length |
| NUMBER | TOTAL_LINE_LENGTH | Total line length |
| NUMBER | TOTAL_LINES | Total lines |
| NUMBER | LINE_DIAMETERS | Line diameters |
| NUMBER | MAX_LINE_LENGTH_WITH_RISERS | Max. line length with risers |
| NUMBER | RISERS_LENGTH | Risers length |
| STRING | MINI_WING_CHARACTER | Mini Wing Character |
| NUMBER | MIN_SINK_RATE | Min. sink rate |
| NUMBER | SEATS | Seats |
| BOOL | SHOCK_AND_LOAD_TEST | Shock and load test |
| NUMBER | BRIDLE_HEIGHT | Distance to risers |
| STRING | CERTIFICATION_NUMBER | Certification number |
| STRING | CERTIFICATION_PROCEDURES | Certification procedures |
| BOOL | CERTIFICATION_FOLDING_LINES_USED | Folding lines used for certification |
```

### The attribute format

**The principles**

* There are three different kinds of attributes
  * Number attributes: Often have a unit like _m_, _mm_, _kg_. May be a number range too. Can have a number variance (+/-).
  * Bool attributes: Yes / No
  * String attributes: For attributes like `CERTIFICATON`: `LTF/EN-B`.
* All attribute values are optional (different paraglider sizes may not have one or the other attribute)
* All attributes have an optional `additionalInfo` to provide more details like `extended` / `certified` / `only when accelerating`.

**Definition**

Using a type system called [Flow](https://flow.org/en/), we can describe the different attribute types.

```
// @flow

type AttributeType =
  | StringAttributeType
  | NumberAttributeType
  | BoolAttributeType;

type StringAttributeType = {
  name: string,
  value: ?string,
  additionalInfo?: string
};

type BoolAttributeType = {
  name: string,
  value: ?boolean,
  additionalInfo?: string
};

type NumberAttributeType = {
  name: string,
  value: ?(number | RangeType),
  valueVariance?: number,
  unit?: string, // If no unit, then it's probably a "count"
  additionalInfo?: string
};

type RangeType = {
  from: number,
  to: number
};
```
