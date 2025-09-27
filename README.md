# Natural Language to SQL Generation using Gemini API
### A DBMS Semester Assignment

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/YourUsername/YourRepoName/blob/main/your_notebook.ipynb)
This project, developed for a Database Management Systems (DBMS) course, demonstrates a sophisticated system for converting natural language questions into executable SQL queries using Google's Gemini API.

---

## 📖 Project Overview

This system allows a user to interact with a database using plain English, which is then translated into accurate, syntactically correct SQL.

The core of the project is an advanced ML-Based approach using Google's Gemini 1.5 Flash model, which successfully fulfills a wide spectrum of query complexities.

### ✨ Key Features & Capabilities
* **Basic Queries:** Handles single-table selections and multi-condition filtering using `AND`/`OR`.
* **Core SQL Operations:** Performs aggregations like `COUNT` and `AVG`, sorting with `ORDER BY`, and grouping with `GROUP BY`.
* **Multi-Table Joins:** Generates queries with `JOIN` operations to retrieve data from multiple tables.
* **Robust Intent Understanding:** Correctly interprets user intent through synonym handling and processes specific data types like dates.
* **Advanced Logic:** Generates complex comparative queries and nested queries using subqueries.

---

## 🛠️ Methodology and Technology

The development of this project involved a significant evolution in approach. The initial plan to use community-hosted models from Hugging Face was abandoned due to instability and connection issues within the Google Colab environment.

The final, robust solution pivots to **Google's Gemini API** for several key reasons:
* **Reliability:** Using Google's native AI service within a Colab environment guarantees stable network access.
* **State-of-the-Art Performance:** The **Gemini 1.5 Flash** model is a powerful, instruction-tuned LLM that excels at reasoning and code generation, making it ideal for high-accuracy Text-to-SQL translation.
* **Contextual Understanding:** The model's effectiveness is significantly enhanced by providing the database schema in the form of `CREATE TABLE` statements. This **prompt engineering** technique gives the AI the precise context it needs to generate accurate queries.

---

## ⚙️ How It Works

The system operates on a simple yet powerful principle:

1.  **Schema Definition:** The database structure is defined using standard `CREATE TABLE` statements.
2.  **Prompt Engineering:** A detailed prompt is constructed containing the user's natural language question and the complete database schema.
3.  **API Call:** This structured prompt is sent to the Gemini API.
4.  **SQL Generation:** The Gemini model analyzes the request and the provided schema to generate a corresponding, syntactically correct SQL query.

---

## 🚀 How to Run This Project

This project is designed to be run in a Google Colab environment. Click the "Open in Colab" badge at the top of this README to get started.

### 1. Set Up Your Google AI API Key
To connect to the Gemini model, you need a free API key.

1.  **Get the Key:**
    * Go to **[Google AI Studio](https://aistudio.google.com/)**.
    * Click `Create API key in new project`.
    * Copy the new key that is generated.
2.  **Add the Key to Colab Secrets:**
    * In the Colab notebook, click the **key icon (🔑)** on the left sidebar to open the "Secrets" panel.
    * Click **+ Add a new secret**.
    * Enter the details exactly as follows:
        * **Name:** `GOOGLE_API_KEY`
        * **Value:** Paste the key you just copied.
    * Make sure the **'Notebook access'** toggle is switched on.

### 2. Run the Main Project Cells
Execute the two primary project cells labeled "Main Project Cell-1" and "Main Project Cell-2". This will:
* Install all necessary libraries.
* Configure the connection to the Gemini API using your key.
* Define the database schema and run all pre-defined test cases.

### 3. Use the Interactive Custom Schema Tester
Run the final cell in the notebook, "Interactive Custom Schema Tester". This powerful tool allows you to:
* Input any database schema using `CREATE TABLE` statements.
* Ask questions in natural language about your custom tables to see the system adapt on the fly.

---

## 💡 Demonstration: Example Queries

The notebook runs a series of predefined test cases to validate the system. Here are some examples of the generated SQL:

**Natural Language:** `Show student names with their course names`
```sql
SELECT
  students.name,
  courses.course_name
FROM students
INNER JOIN courses
  ON students.id = courses.student_id;
```

**Natural Language:** `Find students with marks higher than Priya's`
```sql
SELECT *
FROM students
WHERE marks > (SELECT marks FROM students WHERE name = 'Priya');
```

**Natural Language:** `Find students with marks greater than the average`
```sql
SELECT *
FROM students
WHERE marks > (SELECT AVG(marks) FROM students);
```

**Natural Language:** `Who is the oldest student?`
```sql
SELECT name
FROM students
ORDER BY age DESC
LIMIT 1;
```
