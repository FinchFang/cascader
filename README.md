# cascader.js
级联选择器，当一个数据集合有清晰的层级结构时，可通过级联选择器逐级查看并选择
### 开始：
```html
<script src="./cascader.js"></script>
```
### 示例：
实现一个省市区选择器
> 引入数据源
```html
<script src="china-area.js"></script>
```
> html
```html
<div id="region">
  <select></select>
  <select></select>
  <select></select>
</div>
```
> 实例化
```js
var picker = new Cascader({
  elements: document.querySelectorAll('#region select'),
  data: chinaAreaData,
  initValue: ['广东省', '深圳市', '南山区'],   // [440000, 440300, 440305]
  placeholder: ['请选择省份', '请选择城市', '请选择区域']
})
```
##### 参数：options `{Object}`
| 选项 | 说明 | 类型 | 必填 |
| :--- | :--- | :---: | :---: |
| elements | 用于实例化控件的 select 元素集合 | Array | 是 |
| data | 数据源 | Array | 是 |
| initValue | 初始化的值，可以是 value，也可以是 label | Array | 否 |
| placeholder | 占位符，设置索引对应的 select 元素的第一项 option，默认都是 `请选择` | Array | 否 |
##### 方法：setData
设置数据源
```js
picker.setData([]);   // 参数同 data
```
##### 方法：setValue
设置选中的值
```js
picker.setValue(['北京市']);   // 参数同 initValue
```
##### 方法：getValue
获取选中的值
```js
picker.getValue();
```
返回结果：
```text
{
  index: [],
  value: [],
  label: []
}
```
### Polyfill
代码使用了 Array 的 `forEach`、`findIndex` 方法，如运行的浏览器不支持，你需要添加 polyfill
```html
<script src="./polyfill.js"></script>
```
### Data format
```js
export default [
  {
    value: 110000,
    label: "北京市",
    children: [
      // more ...
    ]
  }
  // more ...
]
```
### Tip
1. 如需监听 `change` 事件，请自行绑定 
2. 数据设置为外置引入的方式，是为了更灵活的使用此插件类
3. 控制数据的层级深度由创建实例时传递的 `select` 元素的数量决定，而不是数据本身的深度
