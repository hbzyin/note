### angular component元数据

|序号 | 名称          |类型              |必要性  | 作用         |示例|备注|
|----|---------------|---------------- |-------|-------------|----|----|
|1   | template       |string           |必须   |组件内联html模板|||
|2   | templateUrl    |string           |必须   |组件外联html模板 |||
|3   | styles         |strtin[]         |非必须 |组件内联css样式 |||
|4   | styleUrls      |string[]         |非必须 |组件外联css样式 |||
|5   | moduleId       |string           |非必须 |组件的组件id    |||
|7   | encapsulation  |ViewEncapsulation|必须   |组件的封装模式   |||
|8   | viewProviders  |Provider[]       |非必须 |组件依赖注入的服务|||
|9   | animations     |any[]            |非必须 |组件级别的动画定义|||
|10  | interpolation  |[string,string]  |非必须 ||||
|11  | entryComponents|Array<any[]>     |非必须 ||||
