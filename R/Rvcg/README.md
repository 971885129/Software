
* 报错

      In file included from vcglib/vcg/complex/complex.h:57:0,
                 from typedef.h:9,
                 from Risolated.cpp:6:
      vcglib/vcg/complex/algorithms/update/selection.h: In instantiation of ‘static size_t vcg::tri::UpdateSelection<ComputeMeshType>::TetraClear(vcg::tri::UpdateSelection<ComputeMeshType>::MeshType&) [with ComputeMeshType = MyMesh; size_t = long unsigned int; vcg::tri::UpdateSelection<ComputeMeshType>::MeshType = MyMesh]’:
      vcglib/vcg/complex/algorithms/update/selection.h:268:15:   required from ‘static void vcg::tri::UpdateSelection<ComputeMeshType>::Clear(vcg::tri::UpdateSelection<ComputeMeshType>::MeshType&) [with ComputeMeshType = MyMesh; vcg::tri::UpdateSelection<ComputeMeshType>::MeshType = MyMesh]’
      Risolated.cpp:96:34:   required from here
      vcglib/vcg/complex/algorithms/update/selection.h:257:4: error: no matching function for call to ‘ForEachTetra(vcg::tri::UpdateSelection<MyMesh>::MeshType&, vcg::tri::UpdateSelection<ComputeMeshType>::TetraClear(vcg::tri::UpdateSelection<ComputeMeshType>::MeshType&) [with ComputeMeshType = MyMesh; size_t = long unsigned int; vcg::tri::UpdateSelection<ComputeMeshType>::MeshType = MyMesh]::__lambda1)’
         });


      make: *** [Risolated.o] Error 1
      ERROR: compilation failed for package ‘Rvcg’
      * removing ‘/media/sdc/tools/software/R/3.6.1/lib64/R/library/Rvcg’

      The downloaded source packages are in
         ‘/tmp/RtmpJNsQp9/downloaded_packages’
      Updating HTML index of packages in '.Library'
      Making 'packages.html' ... done
      Warning message:
      In install.packages("Rvcg") :
        installation of package ‘Rvcg’ had non-zero exit status
      
      # 解决
      切换GCC到更新版本
      Hi, I would like to report that I also encountered this error, and after I switched from gcc-4.8.5 to gcc-5.5.0, the error is gone. Hope it will help.
      module load gcc/5.5.0
