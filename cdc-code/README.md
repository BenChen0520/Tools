名称: 自动生成cdc代码
描述: 增量的从hive传输数据到es

输入: 表名
输出：两个代码分别生成_ss和_ss_delta表


需要的配置（cfg目录下）

    ##指定分区键（必须）
    partition_column XXXXXX
    
    ##指定一个主键（必须）,cdc工具只接受一个主键列
    pk_name XXXXXX
    
    ##主键生成方式（必须）
    pk_format   XXXXXX
    
    ## 中间临时表的名字,（可选） 默认是${table_name}_ss
    ss_table XXXXXX

举例

1. 克隆repository
   git clone git@github.com:BenChen0520/Tools.git

2. 创建所需的目录

   cd Tools/cdc-code
   mkdir cfg dol ddl tmp 

3. 创建CFG文件

    cd cfg
    touch dpdm_wide_snapshot_d_forum_user_note_info.cfg

    输入如下：

    ##指定分区键（必须）
    partition_column hp_cal_dt
    
    ##指定一个主键（必须）,cdc工具只接受一个主键列
    pk_name dt_note_user_pk
    
    ##主键生成方式（必须）
    pk_format   CONCAT(cal_dt,'-',note_id,'-',user_id)
    
    ## 中间临时表的名字,（可选） 默认是${table_name}_ss
    ss_table dpdm_wide_snapshot_d_forum_user_note_info_ss

4. 运行
   cd ../
   ./bin/gen dpdm_wide_snapshot_d_forum_user_note_info

5 查看结果
  cd dol/
  ls -l *dpdm_wide_snapshot_d_forum_user_note_info_ss*



