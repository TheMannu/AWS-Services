### **Database Installation and Setup**

#### a. **MySQL Installation (Ubuntu)**
```bash
sudo apt update
sudo apt install mysql-server
sudo mysql_secure_installation
sudo systemctl start mysql
sudo systemctl enable mysql
```

#### b. **PostgreSQL Installation (Ubuntu)**
```bash
sudo apt update
sudo apt install postgresql postgresql-contrib
sudo systemctl start postgresql
sudo systemctl enable postgresql
sudo -u postgres psql
```

#### c. **MongoDB Installation (Ubuntu)**
```bash
wget -qO - https://www.mongodb.org/static/pgp/server-4.4.asc | sudo apt-key add -
echo "deb [ arch=amd64,arm64 ] https://repo.mongodb.org/apt/ubuntu focal/mongodb-org/4.4 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-4.4.list
sudo apt update
sudo apt install -y mongodb-org
sudo systemctl start mongod
sudo systemctl enable mongod
```

#### d. **Redis Installation (Ubuntu)**
```bash
sudo apt update
sudo apt install redis-server
sudo systemctl enable redis-server
sudo systemctl start redis-server
```

### **Database Queries and Commands**

#### a. **Basic SQL Queries (MySQL/PostgreSQL)**
- **Select Data**: 
  ```sql
  SELECT * FROM table_name;
  ```
- **Insert Data**:
  ```sql
  INSERT INTO table_name (column1, column2) VALUES (value1, value2);
  ```
- **Update Data**:
  ```sql
  UPDATE table_name SET column1 = value1 WHERE condition;
  ```
- **Delete Data**:
  ```sql
  DELETE FROM table_name WHERE condition;
  ```
