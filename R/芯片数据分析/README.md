# 芯片数据分析

#### Affy芯片自定义CDF环境方法

获取目前芯片所需的GDF环境名称

    file<-list.files(path="data/",pattern=".CEL.gz",ignore.case=TRUE,full.names=TRUE)
    #获取CDF name
    cleancdfname(whatcdf(file[1]))
    [1] "glycov3mmcdf"
    
创建CDF环境，环境赋值给变量，变量名为上一步获取的CDF环境名称

    glycov3mmcdf <- make.cdf.env('data/GPL11096_GLYCOv3_Mm.CDF.gz',compress = T)

其他方法，详见makecdfenv包使用说明

#### Affy芯片数据处理

识别芯片所需注释包

    annotate包
    annPkgName(DATA@annotation,type="db")

利用annotate识别出的注释包对芯片进行注释（需确定注释包名称是否有差别）

    eset <- annotateEset(DATA.rma,hgu133plus2.db)
    annotation <- pData(featureData(eset))

olig包标准化

    # 背景校正
    oligo::backgroundCorrectionMethods()#展示有哪些校正方法
    [1] "rma"  "mas"  "LESN"
    bgdata <- backgroundCorrect(DATA,method = 'mas')
    
    # 组间标准化
    normalizationMethods()#展示有哪些标准化方法
    [1] "quantile"           "quantile.robust"    "quantile.in.blocks" "qspline"            "loess"              "invariantset" 
    [7] "constant" 
    normData <- normalize(bgdata)#默认为quantile normalization




