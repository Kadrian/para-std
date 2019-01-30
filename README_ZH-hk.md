# para-std

滑翔傘傘具參數標準和建議

-----------

[English](/README.md)  |  [简体中文](/README_ZH-cn.md)   |  [繁體中文](/README_ZH-hk.md)

-----------

![滑翔傘飛行員夜飛中](/nicolas-tissot-435976-unsplash.jpg)
<sup>Nicolas Tissot 拍攝發佈於Unsplash</sup>

## 滑翔傘標準熟悉

一套滑翔傘可以用許多屬性來描述。

不同的製造商使用不同的屬性名稱。例如`起飛重量`和`飛行重量`是相同的，只是名稱不同。所以飛行員對比滑翔傘傘具就比較困難。

[Kadrian](//github.com/Kadrian) 在搭建[gliderbase.com](//gliderbase.com) 網站的時候需要一套方便資料對比、機器可讀的格式來描述一套滑翔傘。

Kadrian提出了一種用JSON格式描述一套滑翔傘傘具的資料標準。

**致製造商/傘具生產廠商**：請對這套數據標準評論和改進，也希望各廠商能採用這套數據標準，推動資料標準化，完善產業結構。

## 滑翔傘傘具參數標準

### 示例

由廠商**Great Wings Inc.** 生產的一套名為 **Wing 123** 的
**S** 號滑翔傘傘具。
傘具認證型號為 **LTF/EN-A**, 傘面面積為 **24 m<sup>2</sup>**，**certified takeoff weight/認證起飛重量** 為 **90 kg** 至 **120 kg**。
並且帶一套 **trimmer/調整** 系統。

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

### 可選的屬性名稱

這裡寫一些可選的傘具參數，比如增加飛行員可能會感興趣的屬性。這涵蓋了滑翔傘製造商為新傘具增加的一些參數。

目前，這些屬性主要涉及：

* 滑翔傘形狀簡述
* 滑翔機飛行特性
* 滑翔傘安全性能

尤其是傘具的材質還沒有覆蓋。歡迎您增加標準中的其他參數。

**常用參數**

| Usual type | Name                   | English description    | 中文                   |
| ---------- | ---------------------- | ---------------------- | ---------------------- |
| NUMBER     | TAKEOFF_WEIGHT         | Takeoff weight         | 起飛重量               |
| NUMBER     | GLIDER_WEIGHT          | Glider weight          | 傘具重量               |
| NUMBER     | CELLS                  | Cells                  | 傘格數量               |
| NUMBER     | AREA_FLAT              | Flat area              | 展開面積               |
| NUMBER     | AREA_PROJECTED         | Projected area         | 投影面積               |
| NUMBER     | SPAN_FLAT              | Flat span              | 傘翼長度               |
| NUMBER     | SPAN_PROJECTED         | Projected span         | 投影翼長               |
| NUMBER     | ASPECT_RATIO_FLAT      | Flat aspect ratio      | 展開翼弦比*            |
| NUMBER     | ASPECT_RATIO_PROJECTED | Projected aspect ratio | 投影翼弦比*            |
| NUMBER     | LINE_DIAMETERS         | Line diameters         | 線繩直徑               |
| NUMBER     | TOTAL_LINE_LENGTH      | Total line length      | 線繩長度               |
| NUMBER     | CHORD                  | Chord                  | 傘弦長度               |
| STRING     | CERTIFICATION          | Certification          | 認證級別               |

**非常用參數，部分廠商常提供資料**

| Usual type | Name                        | English description          | 中文                         |
| ---------- | --------------------------- | ---------------------------- | ---------------------------- |
| NUMBER     | SPEED_TRIM                  | Trim speed                   | 配平/常規速度*                |
| NUMBER     | SPEED_MAX                   | Max. speed                   | 最高速度                      |
| NUMBER     | MAX_TRAVEL_TRIMMER          | Max. trimmer travel          | 最大配平量*                   |
| NUMBER     | MAX_TRAVEL_ACC              | Max. accelerator travel      | 最大加速度                    |
| BOOL       | HAS_ACC_SYSTEM              | Has accelerator system       | 是否有加速系統                 |
| NUMBER     | TRIMMER_LENGTH              | Trimmer length               | 調整長度*                     |
| NUMBER     | TOTAL_LINES                 | Total lines                  | 線繩數量                      |
| NUMBER     | RISERS_LENGTH               | Risers length                | 承重繩長度                    |
| NUMBER     | BRIDLE_HEIGHT               | Distance to risers           | 座繩長度*                     |
| STRING     | RISERS                      | Risers                       | 承重繩材質                    |
| NUMBER     | MAX_LINE_LENGTH_WITH_RISERS | Max. line length with risers | 最大承重                      |

**較少使用，極少數廠商提供**

| Usual type | Name                             | English description                  | 
| ---------- | -------------------------------- | ------------------------------------ | -------------------- |
| NUMBER     | BEST_GLIDE                       | Best glide                           | 最佳滑翔              |
| NUMBER     | MIN_SINK_RATE                    | Min. sink rate                       | 最小沉降率            |
| NUMBER     | NUMBER_MAIN_LINES                | Number of main lines                 | 主繩數量              |
| STRING     | MINI_WING_CHARACTER              | Mini Wing Character                  | 小傘特徵              |
| BOOL       | HAS_TRIMMER                      | Has trimmer                          | 是否有調整器          |
| NUMBER     | SEATS                            | Seats                                | 座數                  |
| BOOL       | SHOCK_AND_LOAD_TEST              | Shock and load test                  | 負荷衝擊實驗           |
| STRING     | CERTIFICATION_NUMBER             | Certification number                 | 認證編號              |
| STRING     | CERTIFICATION_PROCEDURES         | Certification procedures             | 認證組織              |
| BOOL       | CERTIFICATION_FOLDING_LINES_USED | Folding lines used for certification | 線繩認證              |
| NUMBER     | LINEAR_SCALING_FACTOR            | Linear scaling factor                | 線繩伸縮性能          |
| NUMBER     | LINE_LENGTH                      | Line length                          | 線繩長度              |

### 傘具屬性格式描述

**規則**

* 總共三類屬性
  * 數值型屬性: 經常帶有單位 _m_, _mm_, _kg_。也可能是提供一個資料範圍。可能帶資料誤差 (+/-).
  * 是否型屬性: Yes / No
  * 字串型屬性: 用於描述屬性，比如 `CERTIFICATON/認證級別`: `LTF/EN-B`.
* 所有的傘具屬性均為可選屬性 (不同型號的傘具可能有一個或者其他屬性)
* 所有屬性帶有可選的 `additionalInfo/附加屬性` 來提供更多的資訊 `extended/拓展` / `certified/認證` / `only when accelerating/只在加速過程中`.

**技術規範**

使用[Flow/流](//flow.org/en/)類型系統，我們可以描述不同的屬性類型。

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
