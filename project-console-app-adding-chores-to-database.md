#  Project: Chore Console Application 

## Summary
Build a console application that stores chores in a SQL database.

## Estimated time
Estimated time is five to seven hours.


## Resources to review
- Microsoft - [Create C# apps using SQL Server on Windows](https://www.microsoft.com/en-us/sql-server/developer-get-started/csharp/win)
- Microsoft Docs - [System.Data.SqlClient.dll](https://docs.microsoft.com/en-us/dotnet/api/system.data.sqlclient.sqldatareader?view=dotnet-plat-ext-5.0)
- LinkedIn Learning - [Microsoft SQL server 2019 Essential Training](https://www.linkedin.com/learning/microsoft-sql-server-2019-essential-training)

## Projects
You are building a console application that allows users to store chores in a database.  The minimum viable product will have similar functionality to the previous activity *Create C# apps using SQL Server on Windows.*  Rely heavily on this activity.

### Objectives and requirements

| Project objectives |
| :-- |
| Demonstrate learning through following an example of another project |
| Demonstrate working with a database in a C# console application|

| Minimum Viable Product Requirements |
| :-- |
| When the application runs, create a new database after dropping a previous database with the same name if needed. (You choose the name of the database).   |
| When the application runs, a new table should be created with three columns: 1) ChoreId 2) ChoreName 3) ChoreAssigment |
| When the application runs, three new chores should should be inserted into the database. |
| When the application runs, a chore should be updated |
| When the application runs, a chore should be deleted |
| When the application runs, all chores should be displayed |
| The programming functionality should not live in the Main method. Attempt to break to code into methods|

| (Optional) Additional Features |
| --- |
| Create a console application that allows the user to add, list, and update chores through input in the console. *I.e I can select "Add chore" from a list, type in a chore name and chore assignment.  Then I can print a list of chores to the console.* |

### *Recommended* table 

#### Chores
| Type |Column Name| Notes |
| --- | --- | --- |
| INTEGER | ChoreId | PK (AUTO INCREMENT, UNIQUE) |
| NVARCHAR(MAX)| ChoreName |  |
| NVARChAR(MAX)| ChoreAssignment |  |


#### Example class that would store functionality.
The below class is an example.  There are multiple ways to build this project and you may not be aware of the best practices.  `AddChore()` return type is `int` because this method chooses to return the number of rows updated. 
|  Data Access |
| --- | 
| - connectionSring: string  |
|   |
| + CreateDatabase(): void  |
| + CreateChoreTable(): void  |
| + AddChore(): int  |
| + UpdateChore(): int  |
| + DeleteChore(): int  |
| + GetChores(): List<string>  |

Example
```csharp
public class DataAccess
{
    private string connectionString;

    public DataAccess(string connectionString)
    {
        throw new NotImplementedException();
    }

    public void CreateDatabase()
    {
        throw new NotImplementedException();
    }

    public void CreateChoreTable()
    {
        throw new NotImplementedException();
    }

    public int AddChore()
    {
        throw new NotImplementedException();
    }

    public int UpdateChore()
    {
        throw new NotImplementedException();
    }

    public int DeleteChore()
    {
        throw new NotImplementedException();
    }

    public List<string> GetChores()
    {
        throw new NotImplementedException();
    }
}
```

#### GetChores() Example
The below implementation is *just an example.*  In the below example, GetChores returns  List<string>.  You could write a *GetChores()* method with the return type `void` that is also respnsobie for writing the chores to the console. 

```csharp
// Untested code
public List<string> GetChores()
{
    var chores = new List<string>();

    using (SqlConnection connection = new SqlConnection(connectionString))
    {
        connection.Open();
        var sql = "SELECT ChoreName, ChoreAssignment FROM Chores;";

        using (SqlCommand command = new SqlCommand(sql, connection))
        {

            using (SqlDataReader reader = command.ExecuteReader())
            {
                while (reader.Read())
                {
                    chores.Add($"{reader.GetInt32(0)} {reader.GetString(1)}");
                }
            }
        }

        connection.Close();
    }

    return chores;
}

```

## Recommendations
- The recommend starting point is to first write the SQL statements. Start by writing the create database statement in SQL Server Management Studio.  Next write the create table query in SSMS.  Save all the queries you write. After you have correctly built all your queries, then start the console app application. 

- Expect authentication errors and problems connecting to the database initially.  Quickly reach out to the class if you are unable to diagnose your issue. 
  - Make sure you are using try / catch and look at SQL exceptions.

- Common errors I see include:
  - Forgetting to open the connection
  - Not selecting the database before running certain statements
  - Not creating a valid connection string


