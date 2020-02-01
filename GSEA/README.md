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
    -nperm：1000(Number of permutations)
    -mode:Max_probe
    -rpt_label：输出文件的前缀
    -collapse：false(如果表达数据集文件中NAME已经与gene sets database中名字一致，选择FALSE，反之选择TRUE)
    -norm：meandiv（标准化模式）
    -permute：gene_set-rnd_type no_balance (permutation type)
    -scoring_scheme： weighted(Enrichment statistic)
    -sort：real-order descending(Gene list sorting mode)
    -include_only_symbols：true(Omit features with no Symbol)
    -make_sets：true (Make detailed geneset report)
    -median：false (Median for class metrics)
    -num：100 (Number of Markers)
    -plot_top_x：200 (Plot graphs for the top sets of each Phenotype)
    -metric：Signal2Noise(排序的方法，如果有重复，可以考虑使用T-test；无重复，可以考虑使用Ratio of calsses（差异倍数）或Diff of classes(差异绝对值）)
    -set_max：通路基因的最大数量，默认500，但由于某些通路基因数大于500，建议提高阈值
    -set_min：通路基因的最小数量，默认15
    -out：输出的文件夹
    

### 问题
* 如何确定leading edge gene

