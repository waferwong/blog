
测试
https://gwdev.pawjzs.com/wanjia/app.do?password=abc1234&app_code=10003&mobile=abc1234&appSrc=3&loginType=2&version=1.0
http://127.0.0.1:8080/pinganwj-clinic-h5/login.do?userId=152&ticket=87DF6E6565B9E988D1BDDED62F1400C89F92DD6D&casUuid=7d5e31a6-9af4-4ea7-af2a-d1bd4e85464b


https://gwtest.pawjzs.com/wanjia/app.do?password=xu1024866290&app_code=10003&mobile=xu1024866290&appSrc=3&loginType=2&version=1.0
https://myclinicmtest.pawjzs.com/login.do?userId=163&ticket=7756B1FA873F38178ADCEE8417D8BF552103BBAC&casUuid=6bd8247b-6d84-4929-8199-c8c8f33ba265
https://gwtest.pawjzs.com/wanjia/appAction.do?app_code=10003&password=wj123456&mobile=baibochike001&appSrc=2&loginType=1&source=clinic-app&ticket=&userId=&timestamp=1475981557023&versionName=1.6.0&nonce=885&appType=B&nsukey=gVVTns403IqEo0ijLzWrYpI%2Fg9cLzeYweMngkpFBxbDKzKD8DV7AYHLxNZ6USvFpxOKv5FUoeHZGUiPjzaIhYg%3D%3D

充分考虑便捷操作、异常情况处理、快速找到功能点等等操作性，当然最重要的是保证产品功能和数据、流程无异常。

架构
哪些表示同步过来的？

bug类型
新需求
测试不了解需求
外部接口改变

API开发
清晰的了解是那一块出问题，网关还是server
注意left join还是inner join，尤其是查询别人的表，弄清是否不需要分录【健康产品没有服务项目】

删除html模板数据，容易测试出问题
删除console.log

html
增加maxlength
日期区间限制

# 表
left join baseclinicwj.T_DBC_USER_B b on b.user_id = st.STOCK_USER_ID

# 改善&&问题
utils
format nullable date

枚举



模块
通用or产品包
是否通过参数启用

列表
数据隔离，全部可见还是只创建人本身？
排序
无数据样式

医生、咨询师
按权限去查找or职位or医生表

自测时看下console，解决error，否则会引起其他问题


操作
成功提醒
showMask?


IE8兼容性自检
低网速下重复提交测试

数据测试
对比：0除，除0，整数除，保留位数
多的时候撑满容器
没有任何初始化数据的情况，字典

# 部署

## 字典
### 业务字典
是否各产品包通用？
建表后找林驰雄加，表定义
初始化数据，在管理后台增加后找林驰雄
注意过滤启用，注意停用历史数据的显示问题

## 菜单、权限
insert into T_SYS_RESOURCE (ID, NAME, CODE, TYPE_CODE, INDEX_NUM, PARENT_CODE, LINK_URL, ICON_URL, REMARK, ADD_USER, ADD_DATE, MODIFY_DATE, MODIFY_USER, FLEVEL, DISPLAY, RES_TYPE, DEL_FLAG)
values (SYS_GUID(), '统计报表', 'STATISTIC', 'MODULE', 25, '', '../dentist/dentistClinicIncome.html', 'dentist_report', '', 'USERA002', SYSDATE, null, null, 1, 1, 'B', 0);

insert into T_SYS_RESOURCE (ID, NAME, CODE, TYPE_CODE, INDEX_NUM, PARENT_CODE, LINK_URL, ICON_URL, REMARK, ADD_USER, ADD_DATE, MODIFY_DATE, MODIFY_USER, FLEVEL, DISPLAY, RES_TYPE, DEL_FLAG)
values (SYS_GUID(), '诊所运营', 'STATISTIC01', 'MENU', 1, 'STATISTIC', '../dentist/dentistClinicIncome.html', 'dentist_report', '', 'USERA002', SYSDATE, null, null, 2, 1, 'B', 0);

insert into T_SYS_RESOURCE (ID, NAME, CODE, TYPE_CODE, INDEX_NUM, PARENT_CODE, LINK_URL, ICON_URL, REMARK, ADD_USER, ADD_DATE, MODIFY_DATE, MODIFY_USER, FLEVEL, DISPLAY, RES_TYPE, DEL_FLAG)
values (SYS_GUID(), '收入统计', 'STATISTIC03', 'MENU', 3, 'STATISTIC', '../dentist/dentistIncomeReport.html', 'dentist_report', '', 'USERA002', SYSDATE, null, null, 2, 1, 'B', 0);

insert into T_SYS_RESOURCE (ID, NAME, CODE, TYPE_CODE, INDEX_NUM, PARENT_CODE, LINK_URL, ICON_URL, REMARK, ADD_USER, ADD_DATE, MODIFY_DATE, MODIFY_USER, FLEVEL, DISPLAY, RES_TYPE, DEL_FLAG)
values (SYS_GUID(), '患者分析', 'STATISTIC02', 'MENU', 2, 'STATISTIC', '../dentist/patientAnalysis.html', 'dentist_report', '', 'USERA002', SYSDATE, null, null, 2, 1, 'B', 0);

insert into T_SYS_PERMISSION (ID, RESOURCE_NAME, RESOURCE_CODE, ACTION_NAME, ACTION_CODE, REMARK, ADD_USER, ADD_DATE, MODIFY_USER, MODIFY_DATE, DEL_FLAG)
values (SYS_GUID(), '诊所运营', 'STATISTIC01', '查询', 'VIEW', '', 'USERA002', SYSDATE, null, null, 0);

insert into T_SYS_PERMISSION (ID, RESOURCE_NAME, RESOURCE_CODE, ACTION_NAME, ACTION_CODE, REMARK, ADD_USER, ADD_DATE, MODIFY_USER, MODIFY_DATE, DEL_FLAG)
values (SYS_GUID(), '患者分析', 'STATISTIC02', '查询', 'VIEW', '', 'USERA002', SYSDATE, null, null, 0);

insert into T_SYS_PERMISSION (ID, RESOURCE_NAME, RESOURCE_CODE, ACTION_NAME, ACTION_CODE, REMARK, ADD_USER, ADD_DATE, MODIFY_USER, MODIFY_DATE, DEL_FLAG)
values (SYS_GUID(), '收入统计', 'STATISTIC03', '查询', 'VIEW', '', 'USERA002', SYSDATE, null, null, 0);

select * from  T_SYS_RESOURCE where code = 'STATISTIC' or parent_code = 'STATISTIC'
update  T_SYS_RESOURCE set icon_url = 'dentist_report' where code = 'STATISTIC' or parent_code = 'STATISTIC'
select * from  T_SYS_PERMISSION p where p.resource_code like 'STATISTIC%'
select * from  T_SYS_RESOURCE r where r.name = '体检统计'

public.css
#dentist_report > .side-nav-icon {
    background: url(../images/nav_icon/menu-all-icons.png) 0 -336px no-repeat;
}
#dentist_report.current > .side-nav-icon {
    background: url(../images/nav_icon/menu-all-icons.png) 0 -364px no-repeat;
}

DROP TABLE
create table
alter table T_DWS_PROCESS
  add constraint PK_T_DWS_PROCESS primary key (PROCESS_ID);

# 绩效
1. 完成齿科“处置”前端页面和后台接口开发，关键功能包括：给牙科患者开处置、导入治疗计划、查看历史处置记录、提供打印数据接口等，完成禅道上相关bug修改，功能部署至生产环境。
2. 完成齿科“外加工”前端页面和后台接口开发，关键功能包括：新增加工单、查看/编辑历史加工单等，完成禅道上相关bug修改，功能部署至生产环境。
3. 完成齿科“加工管理”前端页面和后台接口开发，关键功能包括：加工单管理及加工单详情等，完成禅道上相关bug修改，功能部署至生产环境。
完成齿科新功能开发，在细节上完善齿科相关功能。

-- Create table
create table T_MD_CONSULT_TYPE
(
  CONSULT_TYPE_ID   VARCHAR2(36) not null,
  CONSULT_TYPE_CODE VARCHAR2(36),
  CONSULT_TYPE_NAME VARCHAR2(200),
  PY_CODE         VARCHAR2(20),
  WB_CODE         VARCHAR2(20),
  DISABLED        NUMBER(1) default 0,
  REMARK          VARCHAR2(200),
  ADD_USER        VARCHAR2(36),
  ADD_DATE        DATE,
  MODIFY_USER     VARCHAR2(36),
  MODIFY_DATE     DATE,
  PRESET_STATUS   NUMBER(1) default 0,
  DEL_FLAG        NUMBER(1) default 0,
  ORDER_NUM       NUMBER(6)
)
-- Add comments to the table
comment on table T_MD_CONSULT_TYPE
  is '咨询类型表';
-- Add comments to the columns
comment on column T_MD_CONSULT_TYPE.CONSULT_TYPE_ID
  is '咨询类型ID';
comment on column T_MD_CONSULT_TYPE.CONSULT_TYPE_CODE
  is '咨询类型编号';
comment on column T_MD_CONSULT_TYPE.CONSULT_TYPE_NAME
  is '咨询类型名称';
comment on column T_MD_CONSULT_TYPE.PY_CODE
  is '拼音助记词';
comment on column T_MD_CONSULT_TYPE.WB_CODE
  is '五笔助记词';
comment on column T_MD_CONSULT_TYPE.DISABLED
  is '是否可用(0:可用,1:不可用)';
comment on column T_MD_CONSULT_TYPE.REMARK
  is '备注';
comment on column T_MD_CONSULT_TYPE.ADD_USER
  is '记录创建者';
comment on column T_MD_CONSULT_TYPE.ADD_DATE
  is '记录创建日期';
comment on column T_MD_CONSULT_TYPE.MODIFY_USER
  is '记录最新修改者';
comment on column T_MD_CONSULT_TYPE.MODIFY_DATE
  is '记录最新修改时间';
comment on column T_MD_CONSULT_TYPE.PRESET_STATUS
  is '预设标志(0:非预设,1:预设)';
comment on column T_MD_CONSULT_TYPE.DEL_FLAG
  is '逻辑删除标志(0:未删除,1:已删除)';
comment on column T_MD_CONSULT_TYPE.ORDER_NUM
  is '显示顺序';



  -- Create table
create table T_MDC_CONSULT_TYPE
(
  CONSULT_TYPE_ID   VARCHAR2(36) not null,
  CLINIC_ID       VARCHAR2(36) not null,
  P_CONSULT_TYPE_ID VARCHAR2(36),
  CONSULT_TYPE_CODE VARCHAR2(36),
  CONSULT_TYPE_NAME VARCHAR2(200),
  PY_CODE         VARCHAR2(20),
  WB_CODE         VARCHAR2(20),
  DISABLED        NUMBER(1) default 0,
  REMARK          VARCHAR2(200),
  ADD_USER        VARCHAR2(36),
  ADD_DATE        DATE,
  MODIFY_USER     VARCHAR2(36),
  MODIFY_DATE     DATE,
  PRESET_STATUS   NUMBER(1) default 0,
  DEL_FLAG        NUMBER(1) default 0,
  ORDER_NUM       NUMBER(6)
)
-- Add comments to the table
comment on table T_MDC_CONSULT_TYPE
  is '咨询类型表';
-- Add comments to the columns
comment on column T_MDC_CONSULT_TYPE.CONSULT_TYPE_ID
  is '咨询类型ID';
comment on column T_MDC_CONSULT_TYPE.CLINIC_ID
  is '诊所ID';
comment on column T_MDC_CONSULT_TYPE.P_CONSULT_TYPE_ID
  is '平台咨询类型ID';
comment on column T_MDC_CONSULT_TYPE.CONSULT_TYPE_CODE
  is '咨询类型编号';
comment on column T_MDC_CONSULT_TYPE.CONSULT_TYPE_NAME
  is '咨询类型名称';
comment on column T_MDC_CONSULT_TYPE.PY_CODE
  is '拼音助记词';
comment on column T_MDC_CONSULT_TYPE.WB_CODE
  is '五笔助记词';
comment on column T_MDC_CONSULT_TYPE.DISABLED
  is '是否可用(0:可用,1:不可用)';
comment on column T_MDC_CONSULT_TYPE.REMARK
  is '备注';
comment on column T_MDC_CONSULT_TYPE.ADD_USER
  is '记录创建者';
comment on column T_MDC_CONSULT_TYPE.ADD_DATE
  is '记录创建日期';
comment on column T_MDC_CONSULT_TYPE.MODIFY_USER
  is '记录最新修改者';
comment on column T_MDC_CONSULT_TYPE.MODIFY_DATE
  is '记录最新修改时间';
comment on column T_MDC_CONSULT_TYPE.PRESET_STATUS
  is '预设标志(0:非预设,1:预设)';
comment on column T_MDC_CONSULT_TYPE.DEL_FLAG
  is '逻辑删除标志(0:未删除,1:已删除)';
comment on column T_MDC_CONSULT_TYPE.ORDER_NUM
  is '显示顺序';


-----------------------------------------------------------------------------------------------------------------------------------------
prompt  咨询类型表-诊所级   时间：2016-10-18 14:24:37    提交人：汪伟夫
-----------------------------------------------------------------------------------------------------------------------------------------  


CREATE TABLE T_DWS_ONSITE_CONSULT
(
  CONSULT_ID        VARCHAR2(36) NOT NULL,
  CLINIC_ID           VARCHAR2(36) NOT NULL,
  DEPARTMENT_ID       VARCHAR2(36),
  DEPARTMENT_NAME     VARCHAR2(50),
  CONSULTANT_ID           VARCHAR2(36),
  CONSULTANT_NAME         VARCHAR2(50),
  EMPI_ID             VARCHAR2(36),
  TOTAL_PRICE         NUMBER(10,4),
  TREATMENT_TYPE      NUMBER(1),
  CONSULT_TYPE      VARCHAR2(36)
  CONSULT_STATE     NUMBER(1),
  REASON VARCHAR2(150),
  BASE_REQUIREMENT VARCHAR2(90),
  POTENTIAL_REQUIREMENT VARCHAR2(90),
  COMMUNICATION VARCHAR2(1500),
  REMARK              VARCHAR2(200),
  ADD_USER            VARCHAR2(36),
  ADD_DATE            DATE,
  MODIFY_USER         VARCHAR2(36),
  MODIFY_DATE         DATE,
  PRESET_STATUS       NUMBER(1) DEFAULT 0,
  DEL_FLAG            NUMBER(1) DEFAULT 0
)


CREATE TABLE T_DWS_CONSULT_TREATMENT
(
  TREATMENT_ID     VARCHAR2(36) NOT NULL,
  CONSULT_ID     VARCHAR2(36) NOT NULL,
  CLINIC_ID        VARCHAR2(36) NOT NULL,
  POSITION         VARCHAR2(150)
  MD_TREATMENT_ID  VARCHAR2(36),
  DWS_TREATMENT_ID  VARCHAR2(36),
  TREATMENT_NAME   VARCHAR2(200),
  TREATMENT_REMARK VARCHAR2(1500),
  TREATMENT_QTY    NUMBER(6) DEFAULT 1,
  TREATMENT_PRICE  NUMBER(10,4),
  TREATMENT_UNIT  NUMBER(10,4),
  STATUS    NUMBER(2) DEFAULT 0,
  REMARK           VARCHAR2(200),
  ADD_USER         VARCHAR2(36),
  ADD_DATE         DATE,
  MODIFY_USER      VARCHAR2(36),
  MODIFY_DATE      DATE,
  PRESET_STATUS       NUMBER(1) DEFAULT 0,
  DEL_FLAG         NUMBER(1) DEFAULT 0
)


网关gw gateway
Action code
true，需要校验
false，不需要校验


api-server开发流程
接口：
引用上海接口注意dubbo-sh
引用外部接口一定要打印日志
配置：
使用配置文件file:*.properties注意上传
使用新的配置文件时注意spring-config.xml
注意是放在file（机密，服务ip，pwd），还是classpath（业务相关）
版本：
修改api后怎么操作？
改版本号
删除jar包
上传jar包
测试
demo配置
dubbo开发环境配置，不会引用到别人

api
JsonResponse EmptyRsp
api impl
try catch(AppException){log rsp.setError} catch(Exception){log rsp.setError}
注意：@ClinicApi 只是记录日志
这一层不能用java 8 lambda
service
service impl
gateway
接受参数（form 【request body未测试】）
appRequest.getValue
JSON.parseArray(appRequest.getValue("sendSmsMessageReqItems"), SendSmsMessageReqItem.class);

错误排查
服务器内部处理异常
系统繁忙
网关有问题
log.info("response from sendSmsMessage:" + res.toString()); res为空
注意result为null，一个是Exception，

wx
Utils.setCacheTicket
localStorage sessionStorage
测试 json

underscore lodash 实现mybatis resultmap
