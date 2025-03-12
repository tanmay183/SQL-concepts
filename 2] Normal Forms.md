### **Normalization Forms in SQL (with Examples)**
Normalization is a process in SQL used to organize database tables efficiently. It reduces data redundancy and improves data integrity. There are **five primary normal forms** (1NF to 5NF), but most practical databases follow up to **3NF** or **BCNF**.

---

### **1. First Normal Form (1NF)**
✅ **Rule:** Each column should have **atomic values** (indivisible values), and each entry should contain **single values** only.  
✅ **No repeating groups or arrays.**

---

### **Example (Before 1NF - Unnormalized Table)**  
| Student_ID | Name  | Subjects      |
|-------------|--------|----------------|
| 101          | Alice  | Math, Science   |
| 102          | Bob    | English          |

❌ Here, the `Subjects` column has multiple values — **NOT in 1NF**.

---

### **After Applying 1NF**  
| Student_ID | Name  | Subject  |
|-------------|--------|------------|
| 101          | Alice  | Math         |
| 101          | Alice  | Science      |
| 102          | Bob    | English      |

✅ Now each cell has atomic values — **1NF Achieved**.

---

### **2. Second Normal Form (2NF)**
✅ **Rule:** The table must be in **1NF** and all **non-prime attributes** (non-key columns) should depend **entirely on the primary key**.

---

### **Example (Before 2NF - Partial Dependency Exists)**  
| Student_ID | Subject  | Instructor | Department |
|-------------|-----------|------------|----------------|
| 101          | Math       | Mr. Smith   | Science Dept.    |
| 101          | Science    | Dr. John     | Science Dept.    |
| 102          | English    | Ms. Rose     | Arts Dept.        |

❌ The `Department` column depends only on `Subject`, not on the whole primary key `(Student_ID, Subject)` — **NOT in 2NF**.

---

### **After Applying 2NF**  
**Student Table**  
| Student_ID | Subject  | Instructor |
|-------------|-----------|------------|
| 101          | Math       | Mr. Smith   |
| 101          | Science    | Dr. John     |
| 102          | English    | Ms. Rose     |

**Department Table**  
| Subject  | Department     |
|-----------|----------------|
| Math       | Science Dept.  |
| Science    | Science Dept.  |
| English    | Arts Dept.     |

✅ Now, all non-key columns depend only on the primary key — **2NF Achieved**.

---

### **3. Third Normal Form (3NF)**
✅ **Rule:** The table must be in **2NF** and all non-prime attributes should depend **only on the primary key** — **No transitive dependency**.

---

### **Example (Before 3NF - Transitive Dependency Exists)**  
| Student_ID | Name  | City     | Zip_Code |
|-------------|--------|-----------|------------|
| 101          | Alice  | New York  | 10001       |
| 102          | Bob    | Chicago   | 60601       |

❌ `City` depends on `Zip_Code`, not directly on `Student_ID` — **NOT in 3NF**.

---

### **After Applying 3NF**  
**Student Table**  
| Student_ID | Name  | Zip_Code |
|-------------|--------|------------|
| 101          | Alice  | 10001       |
| 102          | Bob    | 60601       |

**Zip_Code Table**  
| Zip_Code | City     |
|------------|-----------|
| 10001      | New York  |
| 60601      | Chicago   |

✅ Now, all non-key attributes depend directly on the primary key — **3NF Achieved**.

---

### **4. Boyce-Codd Normal Form (BCNF)**
✅ **Rule:** The table must be in **3NF**, and for every functional dependency `(X → Y)`, `X` should be a **super key** (a key that uniquely identifies each row).

---

### **Example (Before BCNF - Violating Super Key Rule)**  
| Professor_ID | Course   | Department |
|----------------|-----------|----------------|
| 1              | Math       | Science Dept.  |
| 2              | English    | Arts Dept.      |

❌ Here, `Course → Department`, but `Course` is **not a super key** — **NOT in BCNF**.

---

### **After Applying BCNF**  
**Professor Table**  
| Professor_ID | Course  |
|----------------|-----------|
| 1              | Math       |
| 2              | English    |

**Course Table**  
| Course  | Department     |
|-----------|----------------|
| Math      | Science Dept.  |
| English   | Arts Dept.      |

✅ Now, all dependencies follow the super key rule — **BCNF Achieved**.

---

### **5. Fourth Normal Form (4NF)**
✅ **Rule:** The table must be in **BCNF**, and there should be **no multi-valued dependencies**.

---

### **Example (Before 4NF - Multi-valued Dependency Exists)**  
| Employee_ID | Skill    | Project   |
|----------------|-----------|-----------|
| 101             | Python     | Project A |
| 101             | SQL        | Project A |
| 101             | Python     | Project B |
| 101             | SQL        | Project B |

❌ Skills and projects are independent but still combined — **NOT in 4NF**.

---

### **After Applying 4NF**  
**Employee Skills Table**  
| Employee_ID | Skill    |
|----------------|-----------|
| 101             | Python     |
| 101             | SQL        |

**Employee Projects Table**  
| Employee_ID | Project   |
|----------------|-----------|
| 101             | Project A |
| 101             | Project B |

✅ Now, multi-valued dependencies are separated — **4NF Achieved**.

---

### **6. Fifth Normal Form (5NF) / Project-Join Normal Form (PJNF)**
✅ **Rule:** The table must be in **4NF**, and no data should be lost when the table is split into smaller tables and then joined back.

---

### **Summary Table for Quick Understanding**
| Normal Form | Key Rule                                       | Focus Area             |
|---------------|--------------------------------------------------|-----------------------------|
| **1NF**           | Atomic values (No repeating groups)            | **Data Atomicity**            |
| **2NF**           | No partial dependency on the primary key         | **Eliminate Partial Dependency** |
| **3NF**           | No transitive dependency                          | **Eliminate Transitive Dependency** |
| **BCNF**         | Each determinant must be a super key                | **Stronger Version of 3NF**         |
| **4NF**           | No multi-valued dependency                         | **Handle Multi-Valued Data**        |
| **5NF**           | No data loss after decomposing tables               | **Data Reconstruction**             |

---

### **Which Normal Form Should You Use?**
✅ **1NF, 2NF, and 3NF** are generally sufficient for most applications.  
✅ **BCNF and 4NF** are preferred in complex scenarios requiring high data integrity.  
✅ **5NF** is rare in practical database design.

Would you like practical SQL queries to demonstrate these normalization steps? 🚀
