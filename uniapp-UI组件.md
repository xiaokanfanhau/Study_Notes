# unipp的ui组件整理

- **uni-card卡片**

  **说明**

  ​	只是一个卡片的框架，可以调整宽、高、四周阴影颜色，组件里面写入了<slot></slot>可以在卡片里面添加内容。

  **使用方法**

  - 方式一(基本)：

     ``` javascript
     import uniCard from '@/components/Card/Card.vue'
       	components:{
       		uniCard,
       	},
     ```

  - 方式二(推荐)：放在pages.json文件下

    	`easycom` 组件模式的好处在于不管 `components` 目录下安装了多少组件，`easycom` 打包后会自动剔除没有使用的组件，对组件库的使用尤为友好,组件库批量安装，随意使用，自动按需打包。
    
    ``` javascript
    "easycom": {
      		"autoscan": true,
      		"custom": {
      		// uni-ui 规则如下配置
      		"^uni-(.*)": "@/components/uni-$1/uni-$1.vue" 
      		// 匹配components目录内的vue文件
      		}
      	},
    ```

  **参数信息**

  | 参数            | 类型   | 是否必填 | 默认值  | 说明         |
  | :-------------- | ------ | -------- | ------- | ------------ |
  | width           | String | 否       | 500upx  | 卡片宽度     |
  | height          | String | 否       | 300upx  | 卡片高度     |
  | shadowColor     | String | 否       | #EBEEF9 | 四周阴影颜色 |
  | padding         | String | 否       | 20upx   | 填充大小     |
  | borderRadius    | String | 否       | 3upx    | 边角度       |
  | backgroundColor | String | 否       | #fff    | 背景色       |

- **uni-search搜索框**

  **说明**

  ​	可以随意添加搜索条件数量，设置输入提示文本，返回每一栏的输入信息，搜索按钮只有一个

  **参数信息**

  | 参数        | 类型   | 是否必填 | 默认值                                                       | 说明            |
  | :---------- | ------ | -------- | ------------------------------------------------------------ | --------------- |
  | width       | Number | 否       | 400                                                          | 输入框宽度(upx) |
  | height      | Number | 否       | 50                                                           | 输入框高度(upx) |
  | fold        | Booler | 否       | false                                                        | 是否折叠        |
  | searchArray | Array  | 否       | [<br/>					{<br/>						id:0,<br/>						placeholder:'请输入问题1',<br/>						input:''<br/>					},<br/>					{<br/>						id:1,<br/>						placeholder:'请输入问题2',<br/>						input:''<br/>					}<br/>				] | 搜索数据        |
| fontSize    | Number | 否       | 15                                                           | 字体大小(px)    |
  

**绑定事件**

| 事件        | 说明                 | 返回参数       |
| :---------- | -------------------- | -------------- |
| @inputClick | 点击搜索按钮绑定事件 | 用户输入的信息 |
| @foldTap    | 折叠搜索框           | 状态           |


- **uni-table表格**

  **说明**

  ​	支持调整每一栏的宽度、高度，字体的大小，只需要传入属性值数组，表格内容数组。

  **参数信息**

  | 参数      | 类型   | 是否必填 | 默认值                                                       | 说明                |
  | :-------- | ------ | -------- | ------------------------------------------------------------ | ------------------- |
  | height    | Number | 否       | 100                                                          | 每一栏表格高度(upx) |
  | fontSize  | Number | 否       | 15                                                           | 表格字号(px)        |
  | title     | Array  | 否       | [{<br/>						name: 'id',<br/>						lable: 'id',<br/>						width: 70<br/>					},<br/>					{<br/>						lable: '姓名',<br/>						name: 'name',<br/>						width: 150<br/>					},<br/>					{<br/>						lable: '性别',<br/>						name: 'sex',<br/>						width: 150<br/>					},<br/>					{<br/>						lable: '年龄',<br/>						name: 'age',<br/>						width: 150<br/>					},<br/>					{<br/>						lable: '班级',<br/>						name: 'classroom',<br/>						width: 150<br/>					}<br/>				], | 属性值和宽度(upx)   |
  | tableData | Array  | 否       | [{<br/>						id: 1,<br/>						name: '张三',<br/>						sex: '男',<br/>						age: '18',<br/>						classroom: '三班'<br/>					},<br/>					{<br/>						id: 2,<br/>						name: '李娜',<br/>						sex: '女',<br/>						age: '18',<br/>						classroom: '三班'<br/>					}<br/>				] | 表格内容(对应属性)  |

  **绑定事件**

  | 事件     | 说明               | 返回参数       |
  | :------- | ------------------ | -------------- |
  | @foldTap | 点击打开下拉详情页 | 点击的表格内容 |

- **分页器**

  **说明**

  ​	提供表格的分页功能，按需导入不同的分页功能

  **参数信息**

  | 参数   | 类型   | 是否必填 | 默认值 | 说明                |
  | :----- | ------ | -------- | ------ | ------------------- |
  | height | Number | 否       | 100    | 每一栏表格高度(upx) |

