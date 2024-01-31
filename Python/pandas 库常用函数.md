- **数据读取和写入**
    - `pd.read_csv(file_path)`：从CSV文件中读取数据。
    - `pd.read_excel(file_path)`：从Excel文件中读取数据。
    - `df.to_csv(file_path)`：将数据写入CSV文件。
    - `df.to_excel(file_path)`：将数据写入Excel文件。

- **数据查看**
    - `df.head(n)`：查看DataFrame对象的前n行。
    - `df.tail(n)`：查看DataFrame对象的最后n行。
    - `df.shape()`：查看行数和列数。
    - `df.info()`：查看索引、数据类型和内存信息。
    - `df.describe()`：查看数值型列的汇总统计。
    - `s.value_counts(dropna=False)`：查看Series对象的唯一值和计数。

- **数据清洗**
    - `df.dropna()`：删除包含缺失值的行或列。
    - `df.fillna(value)`：将缺失值填充为指定值。
    - `df.replace(old_value, new_value)`：将指定值替换为新值。
    - `df.duplicated()`：查找重复的行。
    - `df.drop_duplicates()`：删除重复的行。

- **数据筛选**
    - `df[df['column_name'] > value]`：筛选出指定列中大于指定值的行。
    - `df[df['column_name'].isin(list)]`：筛选出指定列中包含在列表中的行。
    - `df.query('expression')`：使用表达式筛选行。
    - `df.loc[row_indexer, column_indexer]`：使用标签筛选行和列。
    - `df.iloc[row_indexer, column_indexer]`：使用整数位置筛选行和列。

- **数据分组和聚合**
    - `df.groupby('column_name').mean()`：按指定列分组并计算平均值。
    - `df.groupby('column_name').sum()`：按指定列分组并计算总和。
    - `df.groupby('column_name').count()`：按指定列分组并计算计数。
    - `df.groupby('column_name').agg(function)`：按指定列分组并应用自定义聚合函数。

- **数据变换**
    - `df.apply(function)`：应用自定义函数到每一列或行。
    - `df.transform(function)`：应用自定义函数到每一个元素。
    - `df.pivot_table(values, index, columns, aggfunc)`：创建透视表。
    - `df.melt(id_vars, value_vars)`：将数据从宽格式转换为长格式。

以上只是一些常用的Pandas函数，还有很多其他的函数和方法可以使用。如果您需要更多的帮助，可以查看以下资源：



