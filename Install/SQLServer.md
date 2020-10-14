# Install SQL Server

```bash
docker pull mcr.microsoft.com/mssql/server:2019-latest

docker run -e "ACCEPT_EULA=Y" -e "SA_PASSWORD=<YourStrong@Passw0rd>" \
   -p 1433:1433 --name sql1 -h sql1 \
   -d mcr.microsoft.com/mssql/server:2019-latest
```

---

# Connect with Visual Studio Code

Install [SQL Server (mssql)](https://marketplace.visualstudio.com/items?itemName=ms-mssql.mssql) extension

Click on `SQL Server` icon and `Add Connection`

Enter the ip and port like this : `localhost,1433`

Use the SQL Login as authentification type. Default user is `SA`

---

Source : 
SQL Server with Docker : https://docs.microsoft.com/en-us/sql/linux/quickstart-install-connect-docker?view=sql-server-ver15&pivots=cs1-bash

Connect with VSCode : https://docs.microsoft.com/en-us/sql/tools/visual-studio-code/sql-server-develop-use-vscode?view=sql-server-ver15
