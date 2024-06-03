CREATING AND ALTERING A DATABASE

Create Database Sample2

sample2.mdf -> contains actial data
sample2_log.ldf -> transaction log dile ~ used to recover the database

change na,e ~ alter database name modfiy name = new database name

Alter Database Sample2 Modify Name = Sample3

another method to change name of database is system stored procedures 
sp = system procedures
sp_renameDB 'Sample3','sample4'


DELETING AND DROPPING A DATABASE

Drop database sample4 ~ this deletes .mdf and .ldf files as well
note that when you are deleting a database it should not be in use ~ we will get an erro as database in use

Drop database sample4

well you want to delete the database that badly !!!
as there are users connected and cant drop it,
put the database in single user mode and then drop the database

Alter Database DatabaseNameSet SINGLE_USER With Rollback Immediate

with roll back immediate option , will rollback all incomplete transactions and closes the connection to the database

Note- system databases cannot be dropped

CREATING TABLES

create table tblgender
(
ID int NOT NULL Primary Key,
Gender nvarchar(50) NOT NULL
)

Use [Database name]
Go # this will automatically take us the the databse specified

To alter and link the two tables via a foreign key we have alter table
Alter table ForeignKeyTable add constraint ForeignKeyTable_ForeignKeyColumn_FK 
FOREIGN KEY (foreignkeycolumn) references Primarykeytable (primaryKeyColumn)

# foreign key helps to enforce Database integrity. it points to a primary key in another table, helps to prevent the invalid data to be inserted into foreign key coloumn


Alter table tblperson add constraint tblperson_GenderID_FK
Foreign Key (GenderID) references tblgender (ID)


Alter table tablename add constraint give_it_a_name_of_the_constraint
Foreign key (which_column_name_needs_to_be_altered) references tablename_to_be_refrred (column_name)

# revision till 3 parts
-- Create the database
CREATE DATABASE review1;
GO

-- Use the newly created database
USE review1;
GO

-- Create the student table
CREATE TABLE student
(
    ID int NOT NULL PRIMARY KEY,
    [name] NVARCHAR(50) NOT NULL,
    genderid INT NOT NULL
);
GO

-- Create the gender table
CREATE TABLE gender
(
    ID int NOT NULL PRIMARY KEY,
    gender NVARCHAR(50) NOT NULL
);
GO

-- Add a foreign key constraint to the student table
ALTER TABLE student 
ADD CONSTRAINT FK_genderid FOREIGN KEY (genderid) 
REFERENCES gender (ID);
GO

view all table
Select * from tblgender
Select * from tblperson

-- insert the data into the table

Insert into tblperson (ID, Name, Email) Values (7, 'Rich', 'r@r.com')

DEFAULT CONSTRAINT


# default value in case anything is not given

# altering an exisiting column to add a default constraint

ALTER TABLE {table_name}
ADD CONSTRAINT {coNSTRAINT_NAME}
DEFAULT {Default_value} FOR {EXISTING_COLUMN_NAME}


Adding a new column with default values to an existing table:
ALTER TABLE {table_name}
ADD {COLUMN NAME}{DATA TYPE}{NULL | NOT NULL}
CONSTRAINT {coNSTRAINT_NAME} DEFAULT {Default_value}

dropping a constraint

ALTER TABLE {TABLE NAME}
DROP CONSTRAINT {CONSTRAINT NAME}

Insert into tblperson (ID, Name, Email, GenderID ) Values (9, 'SARA', 'SA@SA.com', 2)
Insert into tblperson (ID, Name, Email, GenderID ) Values (10, 'JHOnny', 'jO@SA.com',NULL)


ALTER TABLE tblperson 
ADD CONSTRAINT DF_tblperson_genderID
DEFAULT 3 FOR GenderID

ALTER TABLE tblperson 
DROP CONSTRAINT DF_tblperson_genderID

CASCADING REFERENTIAL INTEGRITY CONSTRAINT

-- there is a constrain in which the foreign key pointing to something else cant be deleted
Delete from tblgender where ID = 2 -- thorws no actiton/conflict
No action
Cascade - if attempt is made to delete or update a row with a key referenced by foreign keys in existing rows in other tables, all rows contatining those foreign keys are also deleted or updated

set null - if an attempt is made to delete or update a row with the key referenced by foreign keys in exisiting ros in other tables, all rows contatingi thoses foreign keys wil be set to null

set default ~ similar to above but to a default values

delete from tblgender where ID = 3

CHECK CONSTRAINT
check constrain is used to limit the range of values, that can be enterred for a column. TRUE / False

formula
Alter table {table name}
add constraint {constraint name} check {boolean expression}

alter table tblperson
add Age INT;

-- adding Age column above

Insert into tblperson values


insert into tblperson values (6, 'sala', 's@l.com', 2, -970)

Age > 0 AND Age < 150
adding the constraint as above

Alter table tblperson
Drop constraint CK_tblperson_Age

Alter table tblperson
Add constraint CK_tblperson_Age Check (Age > 0 AND Age < 150)

IDENTITY COLUMN

INSERT INTO tblperson (ID, Name, Email, GenderID, Age)
VALUES 
(8, 'Jane', 'j@l.com', 2, 20),
(11, 'Jione', 'ji@l.com', 3, 10);

IDENTITY COLUMN

if we mark a column as identity column we dont need to supply the column manually it is automatically done by sql

(Is Identity) = Yes
Identity Increment = 1 (we can put anything but best we 1)
Identity Seed = 1 ( starting point we can put the last ID/ primary key log  here i am taking 1 for example
)

we need to make changes, if we want to explicitly supply values in the column that is identity column

error = An explicit value for the identity column in table 'tblperson1' can only be specified when a column list is used and IDENTITY_INSERT is ON.

SET IDENTITY_INSERT tblperson1 ON
insert into tblperson1 (PersonID, Name) values (1, 'jane')

SET IDENTITY_INSERT tblperson1 OFF
insert into tblperson1 values ( 'martin')

-- delete all rows

Delete from tblperson1

after deletin all rows as well the ID will continue after the last entered/continued values and will not start from first

~~~~~~~~~~~

DBCC checkident and reseed start at 0

DBCC CHECKIDENT (tblperson1, RESEED, 0)
insert into tblperson1 values ( 'martin')


LAST GENERATED IDENTITY column value
difference between SCOPE_IDENTITY(), @@IDENTIY AND IDENT_CURRENT('tABLE_NAME')


Select * from Test1
Insert into Test1 Values('y')

select SCOPE_IDENTITY()
select @@IDENTITY

-- writing a trigger -> if any value is entered in test 1 update test 2 with something specified

Create Trigger trForInsert on Test1 for Insert
as
Begin
	Insert into Test2 values('yyzx')
End

Session => new connection to sql server

SCOPE_IDENTITY() - same session and the same scope
@@IDENTITY - same session and across any scope
IDENT_CURRENT('TableName) - specific table across any session and any scope
