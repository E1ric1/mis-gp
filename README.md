# mis-gp
#ER图
![er](https://cloud.githubusercontent.com/assets/16076963/19425892/998b701a-946a-11e6-85ff-18a663c2a55b.PNG)
#axture截图
![axture 2](https://cloud.githubusercontent.com/assets/16076963/19426082/345ca20c-946c-11e6-8f86-8afd3d7ba9f4.PNG)
![axture 3](https://cloud.githubusercontent.com/assets/16076963/19426122/8885395c-946c-11e6-87cd-9df54c05ebcb.PNG)
![axture 4](https://cloud.githubusercontent.com/assets/16076963/19426140/bef08294-946c-11e6-8e6a-6d3120a7f51f.PNG)
![axture 5](https://cloud.githubusercontent.com/assets/16076963/19426179/fde6dda4-946c-11e6-9aad-d752bf4ef26f.PNG)
##sql语句

drop table if exists 保养人person;

drop table if exists 保养消耗;

drop table if exists 保养表table;

drop table if exists 保养记录record;

drop table if exists 保养项目project;

drop table if exists 设备使用;

drop table if exists 设备类型表;

drop table if exists 设备表equipment;

/*==============================================================*/
/* Table: 保养人person                                             */
/*==============================================================*/
create table 保养人person
(
   保养人id                int,
   保养人姓名name            text
);

/*==============================================================*/
/* Table: 保养消耗                                                  */
/*==============================================================*/
create table 保养消耗
(
   保养消耗id               int,
   材料名称                 text,
   材料数量                 float(55)
);

/*==============================================================*/
/* Table: 保养表table                                              */
/*==============================================================*/
create table 保养表table
(
   保养id                 int not null,
   保养编号id               int,
   保养周期type             text,
   保养日期date             date,
   保养人id                int,
   Attribute_13         char(10),
   primary key (保养id)
);

/*==============================================================*/
/* Table: 保养记录record                                            */
/*==============================================================*/
create table 保养记录record
(
   保养编号id               int not null,
   保养id                 int,
   设备id                 int,
   项目id                 int,
   完成情况                 text,
   备注                   text,
   保养记录id               int,
   保养消耗id               int,
   primary key (保养编号id)
);

/*==============================================================*/
/* Table: 保养项目project                                           */
/*==============================================================*/
create table 保养项目project
(
   项目id                 int not null,
   保养编号id               int,
   保养内容content          text,
   设备equip_id           int,
   primary key (项目id)
);

/*==============================================================*/
/* Table: 设备使用                                                  */
/*==============================================================*/
create table 设备使用
(
   设备表_设备id             int,
   设备id                 int,
   设备使用者                text
);

/*==============================================================*/
/* Table: 设备类型表                                                 */
/*==============================================================*/
create table 设备类型表
(
   设备型号id               int not null,
   设备id                 int,
   设备类别名称name           text,
   primary key (设备型号id)
);

/*==============================================================*/
/* Table: 设备表equipment                                          */
/*==============================================================*/
create table 设备表equipment
(
   设备id                 int not null,
   保养编号id               int,
   设备名称name             text,
   设备型号id               int,
   最后保养时间               date,
   primary key (设备id)
);

alter table 保养表table add constraint FK_保养id foreign key (保养编号id)
      references 保养记录record (保养编号id) on delete restrict on update restrict;

alter table 保养表table add constraint FK_保养表id foreign key ()
      references 保养人person on delete restrict on update restrict;

alter table 保养记录record add constraint FK_保养消耗与保养记录 foreign key ()
      references 保养消耗 on delete restrict on update restrict;

alter table 保养项目project add constraint FK_项目id foreign key (保养编号id)
      references 保养记录record (保养编号id) on delete restrict on update restrict;

alter table 设备使用 add constraint FK_设备id foreign key (设备表_设备id)
      references 设备表equipment (设备id) on delete restrict on update restrict;

alter table 设备类型表 add constraint FK_设备类型type foreign key (设备id)
      references 设备表equipment (设备id) on delete restrict on update restrict;

alter table 设备表equipment add constraint FK_设备id foreign key (保养编号id)
      references 保养记录record (保养编号id) on delete restrict on update restrict;
