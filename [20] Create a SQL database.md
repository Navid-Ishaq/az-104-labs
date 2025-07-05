# Lab 20: Create a SQL database

**Duration:** 1h 0m

After logging in with your credentials:

1. Navigate to **Create a resource** from the home page or portal menu.

2. Choose **Databases**, then select **SQL Database**.

3. Fill in the SQL Database form:

   * Select an existing **resource group**.
   * Provide a **database name** (e.g., `MyDatabase`).
   * Click **Create new** under **Server**, then:

     * Enter a unique **server name**.
     * Set **location** to `East US`.
     * Choose **SQL authentication**.
     * Define a **server admin login** (e.g., `DbAdmin`) and **password**.
     * Click **OK** to create the server.
   * Select the newly created server.
   * Set **Want to use SQL elastic pool** to `No`.
   * Under **Compute + Storage**, choose **Basic** tier and click **Apply**.
   * Set **Backup storage redundancy** to **Locally-redundant backup storage**.

4. Proceed to the **Networking** tab and:

   * Set **Connectivity method** to `Public endpoint`.

5. Click **Review + Create**, then click **Create**.

6. After deployment, go to **SQL databases**, then select your new database.

7. From the overview page, click on the **server name** to open the SQL server settings.

8. Go to **Networking**, set **Public network access** to **Selected networks**.

9. Click **+ Add your client IPv4 address** to add your current IP.

10. Enable the checkbox for **Allow Azure services and resources to access this server**.

11. Click **Save** to apply firewall settings.

12. Return to the SQL database blade and select **Query editor**.

13. Sign in using the SQL admin password.

14. In the query editor, paste and run the following script to create four tables:

```sql
-- Create Person table
CREATE TABLE person (
  personid INT IDENTITY PRIMARY KEY,
  firstname NVARCHAR(128) NOT NULL,
  middelinitial NVARCHAR(10),
  lastname NVARCHAR(128) NOT NULL,
  dateofbirth DATE NOT NULL
);

-- Create Student table
CREATE TABLE student (
  studentid INT IDENTITY PRIMARY KEY,
  personid INT REFERENCES person (personid),
  email NVARCHAR(256)
);

-- Create Course table
CREATE TABLE course (
  courseid INT IDENTITY PRIMARY KEY,
  NAME NVARCHAR(50) NOT NULL,
  teacher NVARCHAR(256) NOT NULL
);

-- Create Credit table
CREATE TABLE credit (
  studentid INT REFERENCES student (studentid),
  courseid INT REFERENCES course (courseid),
  grade DECIMAL(5, 2) CHECK (grade <= 100.00),
  attempt TINYINT,
  CONSTRAINT UQ_studentgrades UNIQUE CLUSTERED (studentid, courseid, grade, attempt)
);
```

15. After successful execution, check the **Tables** section to confirm that all four tables were created.

Delete all the resources.



