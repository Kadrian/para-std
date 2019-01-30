# para-std

滑翔伞伞具参数标准和建议

-----------

[English](/README.md)  |  [简体中文](/README_ZH-cn.md)   |  [繁體中文](/README_ZH-hk.md)

-----------

![滑翔伞飞行员夜飞中](/nicolas-tissot-435976-unsplash.jpg)
<sup>Nicolas Tissot 拍摄发布于Unsplash</sup>

## 滑翔伞标准熟悉

一套滑翔伞可以用许多属性来描述。

不同的制造商使用不同的属性名称。例如`起飞重量`和`飞行重量`是相同的，只是名称不同。所以飞行员对比滑翔伞伞具就比较困难。

[Kadrian](//github.com/Kadrian) 在搭建[gliderbase.com](//gliderbase.com) 网站的时候需要一套方便数据对比、机器可读的格式来描述一套滑翔伞。

Kadrian提出了一种用JSON格式描述一套滑翔伞伞具的数据标准。

**致制造商/伞具生产厂商**：请对这套数据标准评论和改进，也希望各厂商能采用这套数据标准，推动数据标准化，完善产业结构。

## 滑翔伞伞具参数标准

### 示例

由厂商**Great Wings Inc.** 生产的一套名为 **Wing 123** 的
**S** 号滑翔伞伞具。
伞具认证型号为 **LTF/EN-A**, 伞面面积为 **24 m<sup>2</sup>**，**certified takeoff weight/认证起飞重量** 为 **90 kg** 至 **120 kg**。
并且带一套 **trimmer/调整** 系统。

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
          "unit": "m²"
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

### 可选的属性名称

这里写一些可选的伞具参数，比如增加飞行员可能会感兴趣的属性。这涵盖了滑翔伞制造商为新伞具增加的一些参数。

目前，这些属性主要涉及：

* 滑翔伞形状简述
* 滑翔机飞行特性
* 滑翔伞安全性能

尤其是伞具的材质还没有覆盖。欢迎您增加标准中的其他参数。

**常用参数**

| Usual type | Name                   | English description    | 中文                   |
| ---------- | ---------------------- | ---------------------- | ---------------------- |
| NUMBER     | TAKEOFF_WEIGHT         | Takeoff weight         | 起飞重量               |
| NUMBER     | GLIDER_WEIGHT          | Glider weight          | 伞具重量               |
| NUMBER     | CELLS                  | Cells                  | 伞格数量               |
| NUMBER     | AREA_FLAT              | Flat area              | 展开面积               |
| NUMBER     | AREA_PROJECTED         | Projected area         | 投影面积               |
| NUMBER     | SPAN_FLAT              | Flat span              | 伞翼长度               |
| NUMBER     | SPAN_PROJECTED         | Projected span         | 投影翼长               |
| NUMBER     | ASPECT_RATIO_FLAT      | Flat aspect ratio      | 展开翼弦比*            |
| NUMBER     | ASPECT_RATIO_PROJECTED | Projected aspect ratio | 投影翼弦比*            |
| NUMBER     | LINE_DIAMETERS         | Line diameters         | 线绳直径               |
| NUMBER     | TOTAL_LINE_LENGTH      | Total line length      | 线绳长度               |
| NUMBER     | CHORD                  | Chord                  | 伞弦长度               |
| STRING     | CERTIFICATION          | Certification          | 认证级别               |

**非常用参数，部分厂商常提供数据**

| Usual type | Name                        | English description          | 中文                         |
| ---------- | --------------------------- | ---------------------------- | ---------------------------- |
| NUMBER     | SPEED_TRIM                  | Trim speed                   | 配平/常规速度*                |
| NUMBER     | SPEED_MAX                   | Max. speed                   | 最高速度                      |
| NUMBER     | MAX_TRAVEL_TRIMMER          | Max. trimmer travel          | 最大配平量*                   |
| NUMBER     | MAX_TRAVEL_ACC              | Max. accelerator travel      | 最大加速度                    |
| BOOL       | HAS_ACC_SYSTEM              | Has accelerator system       | 是否有加速系统                 |
| NUMBER     | TRIMMER_LENGTH              | Trimmer length               | 调整长度*                     |
| NUMBER     | TOTAL_LINES                 | Total lines                  | 线绳数量                      |
| NUMBER     | RISERS_LENGTH               | Risers length                | 承重绳长度                    |
| NUMBER     | BRIDLE_HEIGHT               | Distance to risers           | 座绳长度*                     |
| STRING     | RISERS                      | Risers                       | 承重绳材质                    |
| NUMBER     | MAX_LINE_LENGTH_WITH_RISERS | Max. line length with risers | 最大承重                      |

**较少使用，极少数厂商提供**

| Usual type | Name                             | English description                  | 中文                 |
| ---------- | -------------------------------- | ------------------------------------ | -------------------- |
| NUMBER     | BEST_GLIDE                       | Best glide                           | 最佳滑翔              |
| NUMBER     | MIN_SINK_RATE                    | Min. sink rate                       | 最小沉降率            |
| NUMBER     | NUMBER_MAIN_LINES                | Number of main lines                 | 主绳数量              |
| STRING     | MINI_WING_CHARACTER              | Mini Wing Character                  | 小伞特征              |
| BOOL       | HAS_TRIMMER                      | Has trimmer                          | 是否有调整器          |
| NUMBER     | SEATS                            | Seats                                | 座数                  |
| BOOL       | SHOCK_AND_LOAD_TEST              | Shock and load test                  | 负荷冲击实验           |
| STRING     | CERTIFICATION_NUMBER             | Certification number                 | 认证编号              |
| STRING     | CERTIFICATION_PROCEDURES         | Certification procedures             | 认证组织              |
| BOOL       | CERTIFICATION_FOLDING_LINES_USED | Folding lines used for certification | 线绳认证              |
| NUMBER     | LINEAR_SCALING_FACTOR            | Linear scaling factor                | 线绳伸缩性能          |
| NUMBER     | LINE_LENGTH                      | Line length                          | 线绳长度              |

### 伞具属性格式描述

**规则**

* 总共三类属性
  * 数值型属性: 经常带有单位 _m_, _mm_, _kg_。也可能是提供一个数据范围。可能带数据误差 (+/-).
  * 是否型属性: Yes / No
  * 字符串型属性: 用于描述属性，比如 `CERTIFICATON/认证级别`: `LTF/EN-B`.
* 所有的伞具属性均为可选属性 (不同型号的伞具可能有一个或者其他属性)
* 所有属性带有可选的 `additionalInfo/附加属性` 来提供更多的信息 `extended/拓展` / `certified/认证` / `only when accelerating/只在加速过程中`.

**技术规范**

使用[Flow/流](//flow.org/en/)类型系统，我们可以描述不同的属性类型。

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
