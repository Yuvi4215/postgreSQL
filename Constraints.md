<!-- PostgreSQL README with HTML tags -->
<h1>📘 PostgreSQL Complete Notes (Extended + Constraints Focus)</h1>

<p>This README combines all earlier content with newly added constraint combinations, advanced PostgreSQL features, best practices, and structured explanations.</p>

<h2>🚧 PostgreSQL Constraints (Extended Code Examples)</h2>
<p>This section is now reformatted using <strong>pure HTML</strong> with <code>&lt;h&gt;</code> and <code>&lt;p&gt;</code> tags for every heading and command.</p>

<h3>Basic Constraints</h3>

<h4>Primary Key</h4>
<p><code>CREATE TABLE pk_inline ( id INT PRIMARY KEY, name VARCHAR(50) );</code></p>

<h4>Unique Constraint</h4>
<p><code>CREATE TABLE uniq_inline ( email VARCHAR(100) UNIQUE, username VARCHAR(50) );</code></p>

<h4>NOT NULL Constraint</h4>
<p><code>CREATE TABLE nn_examples ( id INT NOT NULL, name VARCHAR(50) NOT NULL );</code></p>

<h4>CHECK Constraint</h4>
<p><code>CREATE TABLE chk_inline ( age INT CHECK (age &gt;= 18) );</code></p>

<h4>Foreign Key</h4>
<p><code>CREATE TABLE fk_inline ( dept_id INT REFERENCES department(dept_id) );</code></p>

<h3>Alternate Syntax for Constraints</h3>
<p><code>CREATE TABLE pk_table_level ( id INT, name VARCHAR(50), CONSTRAINT pk_id PRIMARY KEY (id) );</code></p>
<p><code>CREATE TABLE uniq_table_level ( email VARCHAR(100), CONSTRAINT unq_email UNIQUE (email) );</code></p>
<p><code>ALTER TABLE student_basic ADD CONSTRAINT chk_roll CHECK (rollno &gt; 0);</code></p>
<p><code>ALTER TABLE student_basic DROP CONSTRAINT chk_roll;</code></p>

<h3>Advanced Constraints</h3>
<p><code>CREATE TABLE composite_pk ( order_id INT, item_id INT, PRIMARY KEY (order_id, item_id) );</code></p>
<p><code>CREATE TABLE composite_unique ( fname TEXT, lname TEXT, UNIQUE (fname, lname) );</code></p>
<p><code>CREATE TABLE deferrable_demo ( id INT PRIMARY KEY, val INT, CHECK (val &gt; 0) DEFERRABLE INITIALLY DEFERRED );</code></p>
<p><code>CREATE DOMAIN positive_int AS INT CHECK (VALUE &gt; 0);</code></p>
<p><code>CREATE TABLE domain_use ( id positive_int, count positive_int );</code></p>
<p><code>CREATE TYPE status_enum AS ENUM ('pending','active','closed');</code></p>
<p><code>CREATE TABLE enum_use ( id INT, status status_enum );</code></p>
<p><code>CREATE TABLE generated_cols ( price NUMERIC, qty INT, total NUMERIC GENERATED ALWAYS AS (price * qty) STORED );</code></p>

<h3>Exclude Constraints</h3>
<p><code>CREATE EXTENSION IF NOT EXISTS btree_gist;</code></p>
<p><code>CREATE TABLE meeting ( emp_id INT, during TSRANGE, EXCLUDE USING GIST ( emp_id WITH =, during WITH &amp;&amp; ) );</code></p>

<h3>Constraint Combinations</h3>
<p><code>CREATE TABLE customer_full ( cust_id SERIAL PRIMARY KEY, fname VARCHAR(50) NOT NULL, lname VARCHAR(50) NOT NULL, email VARCHAR(100) UNIQUE, phone BIGINT UNIQUE, gender VARCHAR(10) CHECK (gender IN ('male','female','other')), created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP, CONSTRAINT name_comb UNIQUE (fname, lname), CONSTRAINT proper_phone CHECK (phone &gt; 6000000000) );</code></p>
<p><code>CREATE TABLE product_full ( product_id SERIAL PRIMARY KEY, product_name VARCHAR(100) NOT NULL, price NUMERIC CHECK (price &gt; 0), quantity INT CHECK (quantity &gt;= 0), category VARCHAR(50), UNIQUE (product_name, category) );</code></p>

<h3>Real-World Combined Constraints</h3>
<p><code>CREATE TABLE auth_user ( id SERIAL PRIMARY KEY, username VARCHAR(50) UNIQUE NOT NULL, password TEXT NOT NULL, email VARCHAR(120) UNIQUE, login_attempts INT DEFAULT 0 CHECK (login_attempts &gt;= 0), CHECK (char_length(password) &gt;= 8) );</code></p>
<p><code>CREATE TABLE inventory ( item_id SERIAL PRIMARY KEY, item_name VARCHAR(100) NOT NULL, sku VARCHAR(50) UNIQUE, stock INT CHECK (stock &gt;= 0), reorder_point INT CHECK (reorder_point &gt;= 0), CHECK (stock &gt;= reorder_point) );</code></p>

<h3>Alternate Syntax Ends</h3>
</h3></h3>
<p>These variations demonstrate table-level constraint definitions and how constraints can be added or removed after table creation.</p>
<pre><code>CREATE TABLE pk_table_level (
    id INT,
    name VARCHAR(50),
    CONSTRAINT pk_id PRIMARY KEY (id)
);

CREATE TABLE uniq_table_level (
    email VARCHAR(100),
    CONSTRAINT unq_email UNIQUE (email)
);

ALTER TABLE student_basic ADD CONSTRAINT chk_roll CHECK (rollno &gt; 0);
ALTER TABLE student_basic DROP CONSTRAINT chk_roll;
</code></pre>

<h3>Advanced Constraints</h3>
<p>These commands include composite keys, deferrable checks, domains, enums, and generated columns for complex validation and structure.</p>
<pre><code>CREATE TABLE composite_pk (
    order_id INT,
    item_id INT,
    PRIMARY KEY (order_id, item_id)
);

CREATE TABLE composite_unique (
    fname TEXT,
    lname TEXT,
    UNIQUE (fname, lname)
);

CREATE TABLE deferrable_demo (
    id INT PRIMARY KEY,
    val INT,
    CHECK (val &gt; 0) DEFERRABLE INITIALLY DEFERRED
);

CREATE DOMAIN positive_int AS INT CHECK (VALUE &gt; 0);

CREATE TABLE domain_use (
    id positive_int,
    count positive_int
);

CREATE TYPE status_enum AS ENUM ('pending','active','closed');

CREATE TABLE enum_use (
    id INT,
    status status_enum
);

CREATE TABLE generated_cols (
    price NUMERIC,
    qty INT,
    total NUMERIC GENERATED ALWAYS AS (price * qty) STORED
);
</code></pre>

<h3>Exclude Constraints</h3>
<p>Exclude constraints prevent overlapping values, commonly used for scheduling, ranges, and spatial data.</p>
<pre><code>CREATE EXTENSION IF NOT EXISTS btree_gist;

CREATE TABLE meeting (
    emp_id INT,
    during TSRANGE,
    EXCLUDE USING GIST (
        emp_id WITH =,
        during WITH &&
    )
);
</code></pre>

<h3>Constraint Combinations</h3>
<p>These examples combine multiple constraints to enforce strong data integrity and structure.</p>
<pre><code>CREATE TABLE customer_full (
    cust_id SERIAL PRIMARY KEY,
    fname VARCHAR(50) NOT NULL,
    lname VARCHAR(50) NOT NULL,
    email VARCHAR(100) UNIQUE,
    phone BIGINT UNIQUE,
    gender VARCHAR(10) CHECK (gender IN ('male','female','other')),
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    CONSTRAINT name_comb UNIQUE (fname, lname),
    CONSTRAINT proper_phone CHECK (phone &gt; 6000000000)
);

CREATE TABLE product_full (
    product_id SERIAL PRIMARY KEY,
    product_name VARCHAR(100) NOT NULL,
    price NUMERIC CHECK (price &gt; 0),
    quantity INT CHECK (quantity &gt;= 0),
    category VARCHAR(50),
    UNIQUE (product_name, category)
);
</code></pre>

<h3>Real-World Combined Constraints</h3>
<p>Realistic scenarios implementing multiple constraints to enforce business rules.</p>
<pre><code>CREATE TABLE auth_user (
    id SERIAL PRIMARY KEY,
    username VARCHAR(50) UNIQUE NOT NULL,
    password TEXT NOT NULL,
    email VARCHAR(120) UNIQUE,
    login_attempts INT DEFAULT 0 CHECK (login_attempts &gt;= 0),
    CHECK (char_length(password) &gt;= 8)
);

CREATE TABLE inventory (
    item_id SERIAL PRIMARY KEY,
    item_name VARCHAR(100) NOT NULL,
    sku VARCHAR(50) UNIQUE,
    stock INT CHECK (stock &gt;= 0),
    reorder_point INT CHECK (reorder_point &gt;= 0),
    CHECK (stock &gt;= reorder_point)
);
</code></pre>
<hr>

<h2>1️⃣ Connecting to PostgreSQL</h2>
<pre><code>psql -U postgres -W</code></pre>

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
<pre><code>CREATE DATABASE mydb;</code></pre>

<h3>Connect to a Database</h3>
<pre><code>\c mydb;</code></pre>
<hr>

<h2>3️⃣ Table Operations</h2>
<h3>Create a Table</h3>
<pre><code>CREATE TABLE student (
    rollno INT,
    name VARCHAR(50),
    address VARCHAR(100),
    percentage NUMERIC(5,2)
);</code></pre>

<h3>List Tables</h3>
<pre><code>\dt;</code></pre>

<h3>Describe Table</h3>
<pre><code>\d student;</code></pre>
<hr>

<h2>4️⃣ ALTER TABLE Commands</h2>
<h3>Add Column</h3>
<pre><code>ALTER TABLE student ADD COLUMN marks INT;</code></pre>

<h3>Add Multiple Columns</h3>
<pre><code>ALTER TABLE student
    ADD COLUMN marks INT,
    ADD COLUMN mobno BIGINT;</code></pre>

<h3>Modify Column Type</h3>
<pre><code>ALTER TABLE student ALTER COLUMN percentage TYPE INT;</code></pre>

<h3>Rename Column</h3>
<pre><code>ALTER TABLE employee RENAME COLUMN address TO city;</code></pre>

<h3>Drop Column</h3>
<pre><code>ALTER TABLE student DROP COLUMN marks;</code></pre>
<hr>

<h2>5️⃣ Constraints (Basic + Advanced)</h2>
<h3>Add Primary Key</h3>
<pre><code>ALTER TABLE student ADD PRIMARY KEY (rollno);</code></pre>

<h3>Add Unique Key</h3>
<pre><code>ALTER TABLE student ADD CONSTRAINT unique_email UNIQUE (email_id);</code></pre>

<h3>Set NOT NULL</h3>
<pre><code>ALTER TABLE student ALTER COLUMN name SET NOT NULL;</code></pre>

<h3>Drop NOT NULL</h3>
<pre><code>ALTER TABLE student ALTER COLUMN name DROP NOT NULL;</code></pre>
<hr>

<h2>6️⃣ Advanced Constraint Types</h2>

<h3>Composite Primary Key</h3>
<pre><code>PRIMARY KEY (order_id, product_id)</code></pre>

<h3>Foreign Key with Actions</h3>
<pre><code>ALTER TABLE employee
ADD CONSTRAINT fk_dept
FOREIGN KEY (dept_id)
REFERENCES department(dept_id)
ON DELETE CASCADE
ON UPDATE SET NULL;</code></pre>

<h3>Multi-Column Unique</h3>
<pre><code>ALTER TABLE student ADD CONSTRAINT uniq_name_address UNIQUE(name, address);</code></pre>

<h3>Advanced CHECK Conditions</h3>
<pre><code>CHECK (percentage BETWEEN 0 AND 100 AND marks >= 0)</code></pre>

<h3>DEFERRABLE Constraints</h3>
<pre><code>ADD CONSTRAINT chk_qty CHECK (quantity > 0) DEFERRABLE INITIALLY DEFERRED;</code></pre>

<h3>Exclude Constraints</h3>
<pre><code>EXCLUDE USING GIST (room WITH =, during WITH &&);</code></pre>

<h3>Domain Constraints</h3>
<pre><code>CREATE DOMAIN percentage_type NUMERIC(5,2) CHECK (VALUE BETWEEN 0 AND 100);</code></pre>

<h3>ENUM Type</h3>
<pre><code>CREATE TYPE gender_enum AS ENUM ('male', 'female', 'other');</code></pre>

<h3>Generated Columns</h3>
<pre><code>fullname VARCHAR(100) GENERATED ALWAYS AS (fname || ' ' || lname) STORED;</code></pre>

<hr>

<h2>7️⃣ Insert, Update, Delete</h2>
<h3>Insert Data</h3>
<pre><code>INSERT INTO student (rollno, name, percentage) VALUES (101, 'Deepak', 70);</code></pre>

<h3>Update</h3>
<pre><code>UPDATE student SET percentage = 80 WHERE rollno = 101;</code></pre>

<h3>Delete</h3>
<pre><code>DELETE FROM student WHERE rollno = 102;</code></pre>
<hr>

<h2>8️⃣ SELECT Queries</h2>
<pre><code>SELECT * FROM student;
SELECT rollno, name FROM student;
SELECT * FROM student WHERE percentage > 70;</code></pre>
<hr>

<h2>9️⃣ PostgreSQL vs MySQL</h2>
<p>Table comparing commands and features.</p>
<hr>

<h2>🔟 Helpful Meta Commands</h2>
<ul>
<li><code>\du</code> – roles</li>
<li><code>\dn</code> – schemas</li>
<li><code>\df</code> – functions</li>
<li><code>\dt+</code> – table details</li>
<li><code>\dy</code> – event triggers</li>
</ul>
<hr>

<h2>1️⃣1️⃣ Auto-Increment Keys</h2>
<pre><code>id SERIAL PRIMARY KEY;</code></pre>
<h3>Identity (Recommended)</h3>
<pre><code>id INT GENERATED ALWAYS AS IDENTITY;</code></pre>
<hr>

<h2>1️⃣2️⃣ Default Values</h2>
<pre><code>ADD COLUMN created_at TIMESTAMP DEFAULT NOW();</code></pre>
<hr>

<h2>1️⃣3️⃣ Check Constraints</h2>
<pre><code>CHECK (percentage BETWEEN 0 AND 100);</code></pre>
<hr>

<h2>1️⃣4️⃣ Foreign Key Example</h2>
<pre><code>REFERENCES department(dept_id);</code></pre>
<hr>

<h2>1️⃣5️⃣ Sorting, Limiting & Pagination</h2>
<pre><code>ORDER BY percentage DESC;
LIMIT 5;
OFFSET 10 LIMIT 5;</code></pre>
<hr>

<h2>1️⃣6️⃣ Pattern Searching</h2>
<pre><code>LIKE 'A%';
ILIKE 'a%';</code></pre>
<hr>

<h2>1️⃣7️⃣ Aggregate Functions</h2>
<pre><code>COUNT(*);
AVG(percentage);
MAX(percentage);
MIN(percentage);</code></pre>
<hr>

<h2>1️⃣8️⃣ Group By & Having</h2>
<pre><code>GROUP BY gender;
HAVING AVG(percentage) > 70;</code></pre>
<hr>

<h2>1️⃣9️⃣ Indexes</h2>
<pre><code>CREATE INDEX idx_student_name ON student(name);
CREATE UNIQUE INDEX idx_email_unique ON student(email_id);</code></pre>
<hr>

<h2>2️⃣0️⃣ Views</h2>
<pre><code>CREATE VIEW high_scores AS
SELECT rollno, name, percentage FROM student WHERE percentage > 75;</code></pre>
<hr>

<h2>2️⃣1️⃣ Copy CSV Import/Export</h2>
<pre><code>COPY student TO '/tmp/student.csv' CSV HEADER;
COPY student FROM '/tmp/student.csv' CSV HEADER;</code></pre>
<hr>

<h2>2️⃣2️⃣ Transactions</h2>
<pre><code>BEGIN;
UPDATE student SET percentage = 100 WHERE rollno = 101;
ROLLBACK;</code></pre>
<hr>

<h2>2️⃣3️⃣ Users & Permissions</h2>
<pre><code>CREATE USER deepak WITH PASSWORD '1234';
GRANT ALL PRIVILEGES ON DATABASE mydb TO deepak;
GRANT SELECT, INSERT ON student TO deepak;</code></pre>
<hr>

<h2>2️⃣4️⃣ Backup & Restore</h2>
<pre><code>pg_dump mydb > backup.sql
psql mydb < backup.sql</code></pre>
<hr>

<h2>2️⃣5️⃣ Advanced Features</h2>
<h3>Table Partitioning</h3>
<pre><code>PARTITION BY RANGE (sale_date);</code></pre>

<h3>Temporary Table</h3>
<pre><code>CREATE TEMP TABLE temp_data (...);</code></pre>

<h3>Unlogged Table</h3>
<pre><code>CREATE UNLOGGED TABLE cache_data (...);</code></pre>

<h3>UPSERT / ON CONFLICT</h3>
<pre><code>ON CONFLICT (rollno) DO UPDATE SET ...;</code></pre>

<h3>Truncate</h3>
<pre><code>TRUNCATE TABLE student RESTART IDENTITY CASCADE;</code></pre>
<hr>

<h2>🎯 Best Practices</h2>
<ul>
<li>Use snake_case naming</li>
<li>Prefer identity columns over SERIAL</li>
<li>Create indexes for frequently used search columns</li>
<li>Use ENUM for fixed value fields</li>
</ul>
<hr>

<p><strong>End of README.</strong></p>

