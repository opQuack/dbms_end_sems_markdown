```
Create table Transaction(
    itemno INTEGER,
    itemname varchar(25),
    rate INTEGER,
    qty INTEGER,
    total INTEGER
);
Create or replace trigger enter_total
Before Insert on Transaction
for each row
BEGIN
    :NEW.total := :NEW.rate * :NEW.qty;
END;
/
insert INTO Transaction values( 1 ,' soap ', 12 , 2 , 0);
insert INTO Transaction values( 2 ,' biscuit ', 25 , 4 , 0);
insert INTO Transaction values( 3 ,' honey ', 30 , 3 , 0);
insert INTO Transaction values( 4 ,' matchstick ', 5 , 6 , 0);
insert INTO Transaction values( 5 ,' chips ', 17 , 5 , 0);
insert INTO Transaction values( 6 ,' cold drinks ', 20 , 1 ,0 );
insert INTO Transaction values( 7 ,' sev ', 5 , 7 , 0);
```


```
Create table Item_Master(
    Itemid INTEGER PRIMARY KEY,
    Description varchar(100),
    Bal_Stock INTEGER
);

Create table Item_Transaction(
    Itemid INTEGER,
    Description varchar(100),
    Quantity INTEGER
);

Create or replace procedure update_balance(x IN INTEGER, y IN INTEGER, z IN varchar)
IS
present INTEGER;
BEGIN
    Select count(*) into present from Item_Master where Itemid = x;
    if (present > 0) then
        Update Item_Master
        set Bal_stock = Bal_stock + y;
    else
        Insert into Item_Master values(x, z, y);
    end if;
END;
/

Create or replace Trigger check_store
Before Insert on Item_Transaction
for each row
BEGIN
    update_balance(:NEW.Itemid, :NEW.Quantity, :NEW.Description);
END;
/

insert INTO Item_Transaction values( 1 ,' dry ', 100 );
insert INTO Item_Transaction values( 2 ,' wet ', 12 );
insert INTO Item_Transaction values( 1 ,' dry ', 50 );
insert INTO Item_Transaction values( 3 ,' wet ', 60 );
insert INTO Item_Transaction values( 4 ,' dry ', 50 );
insert INTO Item_Transaction values( 2 ,' wet ', 6 );
insert INTO Item_Transaction values( 3 ,' wet ', 5 );
```

```
CREATE table temp(
    key INTEGER PRIMARY KEY,
    file_data BFILE
);
CREATE OR REPLACE DIRECTORY
    direct AS 'C:/home'
/
CREATE OR REPLACE PROCEDURE Load_into_blob
AS

    lb  BLOB;
    lf  BFILE := BFILENAME('direct', '/pics');
BEGIN
    INSERT INTO temp (id, file_data)
        VALUES (1, empty_blob())
        RETURNING file_data INTO lBlob;

    DBMS_LOB.OPEN(lFile, DBMS_LOB.LOB_READONLY);

    DBMS_LOB.OPEN(lBlob, DBMS_LOB.LOB_READWRITE);

    DBMS_LOB.LOADFROMFILE(DEST_LOB => lb,
                          SRC_LOB  => lf,
                          AMOUNT   => DBMS_LOB.GETLENGTH(lf));

    DBMS_LOB.CLOSE(lf);
    DBMS_LOB.CLOSE(lb);
END;
/
```



