# Area

### Intro

A three-level linkage selection of provinces and cities, usually used in conjunction with [Popup](#/en-US/popup) component.

### Install

Register component globally via `app.use`, refer to [Component Registration](#/en-US/advanced-usage#zu-jian-zhu-ce) for more registration ways.

```js
import { createApp } from 'vue';
import { Area } from 'vant';

const app = createApp();
app.use(Area);
```

## Usage

### Basic Usage

To initailize `Area` component, `area-list` property is required. Data structure will be introduced later.

```html
<van-area title="Title" :area-list="areaList" />
```

### Initial Value

To have a selected value，simply pass the `code` of target area to `value` property.

```html
<van-area title="Title" :area-list="areaList" value="110101" />
```

### Columns Number

`columns-num` property is used to config number of columns to be displayed. This component has 3 columns corresponding to a 3 level picker by default. Set `columns-num` with 2, you'll have a 2 level picker.

```html
<van-area title="Title" :area-list="areaList" :columns-num="2" />
```

### Columns Placeholder

`columns-placeholder` property is used to config placeholder of columns.

```html
<van-area
  title="Title"
  :area-list="areaList"
  :columns-placeholder="['Choose', 'Choose', 'Choose']"
/>
```

## API

### Props

| Attribute | Description | Type | Default |
| --- | --- | --- | --- |
| value | the `code` of selected area | _string_ | - |
| title | Toolbar title | _string_ | - |
| confirm-button-text | Text of confirm button | _string_ | `Confirm` |
| cancel-button-text | Text of cancel button | _string_ | `Cancel` |
| area-list | Area list data | _object_ | - |
| columns-placeholder | Placeholder of columns | _string[]_ | `[]` |
| loading | Whether to show loading prompt | _boolean_ | `false` |
| readonly | Whether to be readonly | _boolean_ | `false` |
| item-height | Option height, supports `px` `vw` `vh` `rem` unit, default `px` | _number \| string_ | `44` |
| columns-num | Level of picker | _number \| string_ | `3` |
| visible-item-count | Count of visible columns | _number \| string_ | `6` |
| swipe-duration | Duration of the momentum animation，unit `ms` | _number \| string_ | `1000` |
| is-oversea-code | The method to validate oversea code | _() => boolean_ | - |

### Events

| Event | Description | Arguments |
| --- | --- | --- |
| confirm | Emitted when the confirm button is clicked | selected areas |
| cancel | Emitted when the cancel button is clicked | - |
| change | Emitted when current option changed | current values，column index |

### Slots

| Name           | Description                  |
| -------------- | ---------------------------- |
| title          | Custom title                 |
| columns-top    | Custom content above columns |
| columns-bottom | Custom content below columns |

### Methods

Use [ref](https://v3.vuejs.org/guide/component-template-refs.html) to get Area instance and call instance methods.

| Name  | Description               | Attribute       | Return value |
| ----- | ------------------------- | --------------- | ------------ |
| reset | Reset all options by code | _code?: string_ | -            |

### areaList Data Structure

An object contains three properties: `province_list`, `city_list` and `county_list`. Each property is a simple key-value object, key is a 6-bit code of the area of which first two bits stand for the province or state, middle two bits are used as city code and the last two are district code, value is the name of the area. If the code stands for an area that has sub-areas, lower bits of it will be filled with 0.

Example of `AreaList`

```js
export default {
  province_list: {
    110000: 'Beijing',
    330000: 'Zhejiang Province',
  },
  city_list: {
    110100: 'Beijing City',
    330100: 'Hangzhou',
  },
  county_list: {
    110101: 'Dongcheng District',
    110102: 'Xicheng District',
    110105: 'Chaoyang District',
    110106: 'Fengtai District',
    330105: 'Gongshu District',
    330106: 'Xihu District',
    // ....
  },
};
```

Sample data : [Area.json](https://github.com/youzan/vant/blob/dev/src/area/demo/area-en.ts).

### argument of callback function confirm

An array contains selected area objects.

`code` - code of selected area, `name` - name of selected area

```js
[
  {
    code: '330000',
    name: 'Zhejiang Province',
  },
  {
    code: '330100',
    name: 'Hangzhou',
  },
  {
    code: '330105',
    name: 'Xihu District',
  },
];
```
