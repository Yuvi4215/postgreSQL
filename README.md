<h1>📘 PostgreSQL Notes</h1>

<h2>1️⃣ Connecting to PostgreSQL</h2>

<pre><code>psql -U postgres -W
</code></pre>

<h3>Useful Meta Commands</h3>
<ul>
<li><code>\l</code> – list databases</li>
<li><code>\c dbname</code> – connect to database</li>
<li><code>\dt</code> – list tables</li>
<li><code>\d table</code> – describe table</li>
<li><code>\q</code> – quit</li>
</ul>

<hr>

<h2>2️⃣ Database Commands</h2>

<h3>Create a Database</h3>
<pre><code>CREATE DATABASE mydb;
</code></pre>

<h3>Connect to a Database</h3>
<pre><code>\c mydb;
</code></pre>

<hr>

<h2>3️⃣ Table Operations</h2>

<h3>Create a Table</h3>
<pre><code>CREATE TABLE student (
    rollno      INT,
    name        VARCHAR(50),
    address     VARCHAR(100),
    percentage  NUMERIC(5,2)
);
</code></pre>

<h3>List Tables</h3>
<pre><code>\dt;
</code></pre>

<h3>Describe Table</h3>
<pre><code>\d student;
</code></pre>

<hr>

<h2>4️⃣ ALTER TABLE Commands</h2>

<h3>Add Column</h3>
<pre><code>ALTER TABLE student ADD COLUMN marks INT;
</code></pre>

<h3>Add Multiple Columns</h3>
<pre><code>ALTER TABLE student 
    ADD COLUMN marks INT,
    ADD COLUMN mobno BIGINT;
</code></pre>

<h3>Modify Column Type</h3>
<pre><code>ALTER TABLE student 
    ALTER COLUMN percentage TYPE INT;
</code></pre>

<h3>Rename Column</h3>
<pre><code>ALTER TABLE employee 
    RENAME COLUMN address TO city;
</code></pre>

<h3>Drop Column</h3>
<pre><code>ALTER TABLE student DROP COLUMN marks;
</code></pre>

<hr>

<h2>5️⃣ Constraints</h2>

<h3>Add Primary Key</h3>
<pre><code>ALTER TABLE student ADD PRIMARY KEY (rollno);
</code></pre>

<h3>Add Unique Key</h3>
<pre><code>ALTER TABLE student 
    ADD CONSTRAINT unique_email UNIQUE (email_id);
</code></pre>

<h3>Set NOT NULL</h3>
<pre><code>ALTER TABLE student 
    ALTER COLUMN name SET NOT NULL;
</code></pre>

<h3>Drop NOT NULL</h3>
<pre><code>ALTER TABLE student 
    ALTER COLUMN name DROP NOT NULL;
</code></pre>

<hr>

<h2>6️⃣ Insert, Update, Delete</h2>

<h3>Insert Data</h3>
<pre><code>INSERT INTO student (rollno, name, percentage)
VALUES (101, 'Deepak', 70);
</code></pre>

<h3>Insert Missing Columns</h3>
<pre><code>INSERT INTO student (rollno, name)
VALUES (102, 'Ashwini');
</code></pre>

<h3>Update Data</h3>
<pre><code>UPDATE student 
SET percentage = 80 
WHERE rollno = 101;
</code></pre>

<h3>Delete Data</h3>
<pre><code>DELETE FROM student 
WHERE rollno = 102;
</code></pre>

<hr>

<h2>7️⃣ SELECT Queries</h2>

<h3>Select All Rows</h3>
<pre><code>SELECT * FROM student;
</code></pre>

<h3>Select Specific Columns</h3>
<pre><code>SELECT rollno, name FROM student;
</code></pre>

<h3>Conditional Select</h3>
<pre><code>SELECT * FROM student 
WHERE percentage > 70;
</code></pre>

<hr>

<h2>8️⃣ PostgreSQL vs MySQL (Quick Comparison)</h2>

<table>
<thead>
<tr>
<th>Feature</th>
<th>MySQL</th>
<th>PostgreSQL</th>
</tr>
</thead>
<tbody>
<tr>
<td>Describe Table</td>
<td>DESC table;</td>
<td>\d table</td>
</tr>
<tr>
<td>Select Database</td>
<td>USE db;</td>
<td>\c dbname</td>
</tr>
<tr>
<td>Float Type</td>
<td>FLOAT(5,2)</td>
<td>NUMERIC(5,2)</td>
</tr>
<tr>
<td>Modify Column</td>
<td>MODIFY COLUMN</td>
<td>ALTER COLUMN TYPE</td>
</tr>
<tr>
<td>Rename Column</td>
<td>CHANGE COLUMN</td>
<td>RENAME COLUMN</td>
</tr>
<tr>
<td>Reorder Columns</td>
<td>Supported (FIRST/AFTER)</td>
<td>❌ Not supported</td>
</tr>
<tr>
<td>Show Tables</td>
<td>SHOW TABLES;</td>
<td>\dt</td>
</tr>
</tbody>
</table>

<hr>

<h2>9️⃣ Helpful Meta Commands</h2>
<ul>
<li><code>\du</code> – list roles</li>
<li><code>\dn</code> – list schemas</li>
<li><code>\df</code> – list functions</li>
<li><code>\dt+</code> – list tables with details</li>
<li><code>\dy</code> – list event triggers</li>
</ul>

<hr>

<h2>🔟 Best Practices</h2>
<ul>
<li>Use <strong>single quotes</strong> for strings (<code>'text'</code>)</li>
<li>Use <strong>snake_case</strong> naming (PostgreSQL standard)</li>
<li>Prefer <code>SERIAL</code> or <code>BIGSERIAL</code> for auto-increment</li>
</ul>

<pre><code>CREATE TABLE employee (
    id SERIAL PRIMARY KEY,
    name VARCHAR(50) NOT NULL,
    salary NUMERIC(10,2)
);
</code></pre>
<h2>1️⃣ Auto-Increment Keys (SERIAL / BIGSERIAL)</h2>

<pre><code>CREATE TABLE employees (
    id SERIAL PRIMARY KEY,
    name VARCHAR(50),
    salary NUMERIC(10,2)
);
</code></pre>

<h3>Alternative using IDENTITY (recommended)</h3>

<pre><code>CREATE TABLE employees (
    id INT GENERATED ALWAYS AS IDENTITY PRIMARY KEY,
    name VARCHAR(50)
);
</code></pre>

<hr>

<h2>2️⃣ Default Values</h2>

<pre><code>ALTER TABLE student 
ADD COLUMN created_at TIMESTAMP DEFAULT NOW();
</code></pre>

<hr>

<h2>3️⃣ Check Constraints</h2>

<pre><code>ALTER TABLE student 
ADD CONSTRAINT chk_percentage CHECK (percentage BETWEEN 0 AND 100);
</code></pre>

<hr>

<h2>4️⃣ Foreign Key Constraint</h2>

<pre><code>CREATE TABLE department (
    dept_id SERIAL PRIMARY KEY,
    dept_name VARCHAR(50)
);

CREATE TABLE employee (
    emp_id SERIAL PRIMARY KEY,
    emp_name VARCHAR(50),
    dept_id INT REFERENCES department(dept_id)
);
</code></pre>

<hr>

<h2>5️⃣ Sorting, Limiting & Pagination</h2>

<pre><code>SELECT * FROM student ORDER BY percentage DESC;
SELECT * FROM student LIMIT 5;
SELECT * FROM student OFFSET 10 LIMIT 5;
</code></pre>

<hr>

<h2>6️⃣ Pattern Searching (LIKE / ILIKE)</h2>

<pre><code>SELECT * FROM student WHERE name LIKE 'A%';     -- case sensitive
SELECT * FROM student WHERE name ILIKE 'a%';    -- case insensitive
</code></pre>

<hr>

<h2>7️⃣ Aggregate Functions</h2>

<pre><code>SELECT COUNT(*) FROM student;
SELECT AVG(percentage) FROM student;
SELECT MAX(percentage) FROM student;
SELECT MIN(percentage) FROM student;
</code></pre>

<hr>

<h2>8️⃣ Group By & Having</h2>

<pre><code>SELECT gender, COUNT(*) 
FROM student 
GROUP BY gender;

SELECT address, AVG(percentage)
FROM student
GROUP BY address
HAVING AVG(percentage) > 70;
</code></pre>

<hr>

<h2>9️⃣ Creating Indexes (for performance)</h2>

<pre><code>CREATE INDEX idx_student_name ON student(name);
CREATE UNIQUE INDEX idx_email_unique ON student(email_id);
</code></pre>

<hr>

<h2>🔟 Views</h2>

<pre><code>CREATE VIEW high_scores AS
SELECT rollno, name, percentage
FROM student
WHERE percentage > 75;

SELECT * FROM high_scores;
</code></pre>

<hr>

<h2>1️⃣1️⃣ Copy CSV (Import / Export)</h2>

<h3>Export Table → CSV</h3>
<pre><code>COPY student TO '/tmp/student.csv' CSV HEADER;
</code></pre>

<h3>Import CSV → Table</h3>
<pre><code>COPY student FROM '/tmp/student.csv' CSV HEADER;
</code></pre>

<hr>

<h2>1️⃣2️⃣ Transactions (BEGIN / COMMIT / ROLLBACK)</h2>

<pre><code>BEGIN;
UPDATE student SET percentage = 100 WHERE rollno = 101;
ROLLBACK;   -- undo changes

BEGIN;
UPDATE student SET percentage = 95 WHERE rollno = 102;
COMMIT;     -- save changes
</code></pre>

<hr>

<h2>1️⃣3️⃣ Creating Users & Granting Permissions</h2>

<pre><code>CREATE USER deepak WITH PASSWORD '1234';

GRANT ALL PRIVILEGES ON DATABASE mydb TO deepak;

GRANT SELECT, INSERT ON student TO deepak;
</code></pre>

<hr>

<h2>1️⃣4️⃣ Backup & Restore</h2>

<h3>Backup a Database</h3>
<pre><code>pg_dump mydb &gt; backup.sql
</code></pre>

<h3>Restore Database</h3>
<pre><code>psql mydb &lt; backup.sql
</code></pre>

