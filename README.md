# Student Support Dashboard

A simple local website for exploring student performance by subject. It uses Flask, HTML, CSS, and JavaScript. It does not use Streamlit.

## Run it in VS Code

1. Open the `student-performance-web` folder in VS Code.
2. Open **Terminal → New Terminal**. In PowerShell, create the project's Python environment and install its packages:

```powershell
& "$env:LOCALAPPDATA\Programs\Python\Python314\python.exe" -m venv .venv
.\.venv\Scripts\python.exe -m pip install -r requirements.txt
```

3. Start the website:

```powershell
.\.venv\Scripts\python.exe server.py
```

4. Open [http://127.0.0.1:5000](http://127.0.0.1:5000).

Keep the terminal open while using the site. Press **Ctrl+C** to stop it. If Windows cannot find the Python path in the first command, replace it with the location of your installed Python 3.14 `python.exe`.

## What it does

- Choose Applied Data Science, Machine Learning, Data Warehouse and Data Mining, Coding Skills, or Principles of Big Data Management.
- Set the mark cutoff. By default, a mark below 50 out of 100 is labelled at risk.
- Compare Logistic Regression, Decision Tree, and Random Forest.
- Compare accuracy, precision, recall, F1, ROC AUC, and fairness gaps by gender.
- Search the names of students the Random Forest flags in the held-out test group.
- View the actual mark for the selected subject and download the flagged list as a CSV.
- Select a test student and see a SHAP explanation of one model prediction.

## Project dataset

`data/indian_student_performance_demo.csv` is a newly generated, fictional dataset with 600 records. It has Indian-style fictional names, semester, attendance, study hours, assignment and lab completion, participation, marks for all five subjects, and an overall average. It contains no real school records and should not be described as real data from India.

`generate_dataset.py` recreates the synthetic CSV using Python's standard library.

For each analysis, the selected subject's mark is the prediction target. Names, gender, subject marks, and overall average are excluded from model inputs to avoid identity leakage and to avoid using final marks to predict themselves. Gender is kept separately for the fairness check. The at-risk names shown are from the 25% held-out test group whose Random Forest risk estimate meets the chosen alert threshold; the list is not a prediction for every student in the dataset.

## Notes

The dataset uses made-up values and a fixed split to demonstrate the workflow. Its model scores do not show how the system would perform at a real Indian college. A prediction is only a prompt to review a student's situation; it should not decide academic support on its own.

The server listens only on `127.0.0.1` and is for local use. Put it online only after preparing a production setup, reviewing privacy and consent, and choosing a host. Do not upload real student records or secrets to GitHub.
