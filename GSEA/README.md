GSEA

###  输入文件
* 第一列为id或symbol
* 第二列为gene描述信息，这一列将会被忽略，填充内容可为NA
* 其他列为各个样本的表达量数据
* 注意：GSEA输入数据必须是经过标准化的表达量数据


### 参数说明

    -Xmx10000m:设置最大内存10000兆
    -res：表达量文件
    -cls：样本信息
    -gmx：数据库文件
    -nperm：Number of permutations
    -rpt_label：输出文件的前缀
    -collapse：如果表达数据集文件中NAME已经与gene sets database中名字一致，选择FALSE，反之选择TRUE。
    -norm：meandiv
    -permute：
    -scoring_scheme：
    -sort：
    -include_only_symbols：
    -make_sets：
    -median：
    -num：
    -plot_top_x：
    -metric：排序的方法，如果有重复，可以考虑使用T-test；无重复，可以考虑使用Ratio of calsses（差异倍数）或Diff of classes(差异绝对值）
    -plot_top_x：默认20，代表富集分析排名最高的20个通路
    -set_max：通路基因的最大数量，默认500，但由于某些通路基因数大于500，建议提高阈值
    -set_min：通路基因的最小数量，默认15
    -out：输出的文件夹
    

### 问题
* 如何确定leading edge gene

