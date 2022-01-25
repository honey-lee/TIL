# ⚙️TNSNAMES.ORA

## 1. TNSNAMES.ORA?

TNSNMES.ORA is **a configration file that Oracle database use**. It allows users and applications to connect to Oracle Databases by matching a connection name with all of the relevant details.

## 2. Where is the TNSNAMES.ORA located?

> $ORACLE_HOME\network\admin\

- `$ORACLE_HOME` : the location that the Oracle database is installed in.

## 3. How to find ORACLE_HOME and the TNSNAMES.ORA Location in Unix

```powershell
env | grep ORACLE_HOME

echo $ORACLE_HOME
```

## 4. Syntax of the TNSNAMES.ORA File

```powershell
net_service_name =
  (DESCRIPTION=
    (ADDRESS = (PROTOCOL = TCP)(HOST = xxx.xxx.com)(PORT = 1521)
  )
  (CONNECT_DATA =
    (SERVICE_NAME=service_name)
  )
)
```

- **net_service_name**: This is the name that you use for a connection string later. You can choose what this is. It’s like a name you give to this set of connection details.
- **host**: The IP address or server name where the database lives or that you want to connect to.
- **port**: The port that is required for the connection. In most cases the default port of 1521 will be fine.
- **service_name**: This is the name of the database you want to connect to.

## 5. How can I create / modify the TNSNAMES.ORA File?

1. MODIFY

   To add an entry into the file, you can either copy the format from above, or copy and paste an existing entry from the file. Then, make changes.

2. CREATE

   You can also create one if you don’t have it in your ORACLE_HOME directory. To create the file, open a new text file. Save the file with the name TNSNAMES.ORA and save it into your ORACLE_HOME location. Below is the template

   ```powershell
   net_service_name =
     (DESCRIPTION=
       (ADDRESS = (PROTOCOL = TCP)(HOST = xxx.xxx.com)(PORT = 1521)
     )
     (CONNECT_DATA =
       (SERVICE_NAME=service_name)
     )
   )
   ```

## 6. Does SQL Developer use TNSNAMES.ORA

In SQL Developer, you can set the location of your TNSNAMES.ORA file, which will give you additional options when creating connections to database.

1. In SQL Developer, open **Tools > Preferences.**

2. Expand the **Database** section and click on **Advanced**.

   In the TNSNAMES Directory option at the bottom, add the location of the TNSNAMES.ORA file. This will be `ORACLE_HOME\\network\\admin`

<img src="/Users/honeysmacbook/Library/Application Support/typora-user-images/Screenshot 2022-01-23 at 20.50.31.png" alt="Untitled" style="zoom:50%;" />

1. Then, click OK.

   Now you can create a new connection, you can use this TNSNAMES DATA.

2. Click Create New Connection

   <img src="/Users/honeysmacbook/Library/Application Support/typora-user-images/Screenshot 2022-01-23 at 20.50.53.png" alt="Untitled" style="zoom:50%;" />

3. In the connection Type drop-down, select TNS.

4. Selecting TNS will allow you to select your connection details from the TNSNAMES file.

<img src="/Users/honeysmacbook/Library/Application Support/typora-user-images/Screenshot 2022-01-23 at 20.51.15.png" alt="Untitled" style="zoom:50%;" />