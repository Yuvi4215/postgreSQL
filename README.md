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
