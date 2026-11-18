# 🔐 Cybersecurity Analysis in Mexico Using INEGI Data (MOCIBA 2024)

Final project for the **Junior Data Science Course** (Mujer Digital / Junior Achievement México · Tecnolochicas, Fundación Televisa).

A Python analysis of the INEGI *Cyberbullying Module (MOCIBA) 2024* dataset, using its questions about security measures, incidents, and perceived protection. The project covers data cleaning, national estimates with survey expansion factors, visualizations, a choropleth map, a statistical test, and **machine learning** models (K-Means and logistic regression), all wrapped in an interactive menu.

---

## 🎯 Objective

To understand what people in Mexico do to protect themselves online, which incidents they experience, and whether their security measures are actually associated with fewer cybercrimes.

## ❓ Questions Answered

1. What percentage of the population takes security measures?
2. What is the most commonly used security measure?
3. What is the most frequent cybercrime?
4. How does prevention culture vary by state? (choropleth map)
5. How does prevention vary by sex?
6. How effective are the measures? (cross-tabulation, chi-square test, and boxplot)
7. How well does perceived security match reality? (machine learning)

## 📊 Key Results

- **74.17%** of the population adopts at least one security measure.
- The most widely used measure is **creating strong passwords**.
- The most frequent incident is **social media account hacking**.
- **Cybersecurity paradox:** people who take security measures report *more* incidents than those who don't. My interpretation (a hypothesis, not proven by this data): people who protect themselves spend more time online and are better at detecting attacks, while those who don't may not realize they were victims.

## 🤖 Machine Learning

| Technique | Purpose |
|---|---|
| **K-Means** (3 clusters, data scaled with `StandardScaler`) | Segment profiles based on age, whether the person takes security measures, and whether they suffered an incident |
| **Logistic regression** (`class_weight='balanced'`) | Classify whether a person suffered an incident based on their age and whether they take security measures |

**Evaluation:** 70% training / 30% test split, confusion matrix, ROC curve, and 5-fold cross-validation.

**Result:** an AUC of **0.58**, meaning the model performs only slightly better than chance.

**Lessons learned:**
- At first the model was biased: it almost always predicted "No". I fixed this with `class_weight='balanced'`.
- With only two variables (age and security measures), there isn't enough information to predict incidents. To improve the model, I would add more variables (education level, locality size, type of measures, etc.) and try other algorithms.

## 🗂️ Data

- **Source:** [INEGI – Cyberbullying Module (MOCIBA) 2024](https://www.inegi.org.mx/)
- **Size:** 43,434 records; only the columns needed for the analysis were kept.
- National estimates use the survey's **expansion factor**.

> Check INEGI's terms of use before uploading the dataset to the repository. If you don't include it, add the download link here.

## 🧹 Data Cleaning

1. Selected the relevant columns and made a copy of the DataFrame.
2. Renamed columns to `snake_case` (e.g., `P2_1` → `medida_crear_contrasenas`).
3. Filled null values with `0` (a value that doesn't exist in INEGI's data dictionary, so nulls stay identifiable) and converted `float` to `int` to preserve the original coding (1 = Yes, 2 = No, 9 = Don't know / No response).
4. Checked for duplicates (none found).
5. Exported the cleaned dataset to CSV.

## 🖥️ Interactive Menu

```
1. Percentage of the population that does or doesn't take security measures
2. Cybersecurity measures
3. Cybercrimes
4. Prevention culture by state (choropleth map)
5. Security culture by sex
6. Effectiveness of measures and distribution (boxplot)
7. Perception vs. reality (machine learning)
8. Exit
```

Built with functions, a `lambda` function to format figures, a `match-case` structure, and error handling (`try/except`).

## 🛠️ Technologies

Python · pandas · matplotlib · seaborn · SciPy · scikit-learn · geopandas · Google Colab

## ▶️ How to Run

1. Open `PROYECTO_MODULO_3.ipynb` in Google Colab or Jupyter.
2. Download the MOCIBA 2024 dataset from INEGI and update the `file_path` variable in the first cell.
3. Install the dependencies if needed:
   ```bash
   pip install pandas matplotlib seaborn scipy scikit-learn geopandas
   ```
4. Run the cells in order and interact with the menu.

> The notebook uses `google.colab` to clear the screen; if you run it outside Colab, replace that function.

## 📁 Structure

```
├── README.md
└── PROYECTO_MODULO_3.ipynb   # Notebook with the full analysis and model
```

## 🚀 Future Improvements

- Add more variables to the model and compare other algorithms (decision trees, random forest).
- Build a Power BI dashboard with the results.
- Analyze by age group and education level.

## 👩‍💻 Author

**Karla García Marín** · Computer Systems Engineer · Data Analysis and Cybersecurity

📧 karlagm2699@gmail.com · 💼 [LinkedIn](https://www.linkedin.com/in/karla-garcia-marin)
