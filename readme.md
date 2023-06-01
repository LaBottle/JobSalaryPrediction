# **Job Salary Prediction**

## **1. 目标**

推测工作薪水

## **2. 数据集**

|        Name        |   中文名   |  类型(Type)  |
| :----------------: | :--------: | :----------: |
|         ID         |   标识符   | ```int64```  |
|       Title        |    职业    |  ```enum```  |
|  FullDescription   |    描述    | ```string``` |
|    LocationRaw     |    位置    | ```string``` |
| LocationNormalized | 标准化位置 |  ```enum```  |
|    ContractType    |  合同类型  | ```enum?```  |
|    ContractTime    |  合同时间  | ```enum?```  |
|      Company       |    公司    | ```enum?```  |
|      Category      |  职业类别  |  ```enum```  |
|     SalaryRaw      |    工资    | ```string``` |
|  SalaryNormalized  | 标准化工资 | ```int64```  |
|     SourceName     |  信息来源  |  ```enum```  |

    注：`enum?`表示可空枚举

## **3. 步骤**

### **1. 调整列的权重**

使用可视化工具比较各列与SalaryNormalized的相关性。影响较小的列可以直接剔除或降低权重。LocationRaw、SalaryRaw已经有处理好的标准化后的数据，也可以剔除。  
（FullDescription可以通过提取关键词来使其能够进行学习，不过这个可能有点难度，如果时间不够也剔除吧）

### **2. 删除无效数据**

通过检测，我们发现为空的数据项有
|        Name        | NullNumber |
| :----------------: | :--------: |
|         Id         |     0      |
|       Title        |     1      |
|  FullDescription   |     0      |
|    LocationRaw     |     0      |
| LocationNormalized |     0      |
|    ContractType    |   179326   |
|    ContractTime    |   63905    |
|      Company       |   32430    |
|      Category      |     0      |
|     SalaryRaw      |     0      |
|  SalaryNormalized  |     0      |
|     SourceName     |     1      |

ContractType、ContractTime、Company为空数据项较多，可以作为可空数据项处理  
Title和SourceName为空的数据则直接剔除

### **3. 处理可空数据项**

一种可行的方案是对于可空的列再添加一列是否为空作为标识，然后再填充为空项  

### **4. 将数据进行标准化**

对于Title、Company这种数据可以视作枚举，将其转成数字便可进行学习  

### **5. 训练模型**

1. 切分训练集和测试集
2. 使用一种算法进行训练
3. 评估模型准确度
4. 选出最优算法

### **6. 使用模型**

对预测集格式化或使用模型预测薪水

## **4. 制作PowerPoint**

按照整个项目的流程进行制作，重点强调我们所过的努力，比如我们从多个模型中选出了最优模型，而不知直接说我们采用了某个模型，不谈原因。  
制作完成后需要进行预演，确保时间在5分钟之内。

## **5. 撰写报告**

