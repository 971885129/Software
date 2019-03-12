# BLAST
* 1.配置本地BLAST库
NCBI上可以下载nt（核酸） nr（蛋白）库，若已知物种，可下载对应物种的基因组fasta文件或者RNA fasta文件进行建库

        makeblastdb -in rna.fa -dbtype nucl -out has_rna
        -dbtype 为构建库的类型，核酸为nucl，蛋白为prot
        -out 为所建库的名称
* 2.比对

      blastn -query data/ncrna.fa -out result.blast -db /media/sdb/user/wxm/database/NCBI/Mus_musculus/mmu_rna -outfmt 6 -evalue 1e-5 -num_threads 40
* 3.bedtools将BLAST结果注释到gene symbol（在使用NCBI下载的fasta后不需要这一步）
*注意： 导入到bedtools的文件需要对染色体进行排序，否则报错；并且起始坐标要小于终止坐标

