# conda info
显示基本信息
- `conda info -e` 列出已经创建的虚拟环境

# 虚拟环境的使用
## conda activate \<xxx>
激活\<xxx>虚拟环境
## conda deactivate
退出当前虚拟环境，返回父级虚拟环境。如果在`base`虚拟环境中执行，则退出Anaconda命令提示符。

## conda create -n \<name>
创建虚拟环境

## conda remove -n \<name> --all
删除虚拟环境以及该环境的所有信息