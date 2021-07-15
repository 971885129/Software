# gridtext
## 安装
### 报错

    grid-renderer.h:61:94: error: no matching function for call to ‘Rcpp::Vector<10, Rcpp::PreserveStorage>::Vector(int, bool&, const GraphicsContext&)’
### 解决

    gcc版本问题
    module load gcc6-9后安装无报错
