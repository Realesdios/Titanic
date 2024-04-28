<h1 id="load-the-data">Load the data</h1>
<p>df_train = pd.read_csv(“train.csv”)<br>
df_test = pd.read_csv(“test.csv”)</p>
<h1 id="consolidate-datasets-into-one">Consolidate datasets into one</h1>
<p>df = pd.concat([df_train, df_test], axis=0)</p>
<h1 id="handling-missing-values">1. Handling Missing Values</h1>
<h1 id="check-for-missing-values">Check for missing values</h1>
<p>missing_values = df.isnull().sum()</p>
<h1 id="impute-missing-age-values-with-the-median-age-grouped-by-pclass-and-sex">Impute missing ‘Age’ values with the median age grouped by ‘Pclass’ and ‘Sex’</h1>
<p>df[‘Age’] = df.groupby([‘Pclass’, ‘Sex’])[‘Age’].transform(lambda x: x.fillna(x.median()))</p>
<h1 id="remove-or-impute-missing-embarked-values-based-on-the-most-frequent-category">Remove or impute missing ‘Embarked’ values based on the most frequent category</h1>
<p>df[‘Embarked’] = df[‘Embarked’].fillna(df[‘Embarked’].mode()[0])</p>
<h1 id="decide-on-handling-the-cabin-column">Decide on handling the ‘Cabin’ column</h1>
<h1 id="for-example-extract-the-initial-letters-as-a-new-feature">For example, extract the initial letters as a new feature</h1>
<p>df[‘Cabin_initial’] = df[‘Cabin’].str[0]</p>
<h1 id="handling-outliers">2. Handling Outliers</h1>
<h1 id="detect-outliers-in-fare-using-iqr">Detect outliers in ‘Fare’ using IQR</h1>
<p>Q1 = df[‘Fare’].quantile(0.25)<br>
Q3 = df[‘Fare’].quantile(0.75)<br>
IQR = Q3 - Q1<br>
outliers = df[(df[‘Fare’] &lt; Q1 - 1.5 * IQR) | (df[‘Fare’] &gt; Q3 + 1.5 * IQR)]</p>
<h1 id="cap-outliers-or-transform-fare-using-logarithmic-scaling">Cap outliers or transform ‘Fare’ using logarithmic scaling</h1>
<h1 id="for-example-cap-outliers-to-a-certain-threshold">For example, cap outliers to a certain threshold</h1>
<p>df[‘Fare’] = df[‘Fare’].clip(lower=df[‘Fare’].quantile(0.05), upper=df[‘Fare’].quantile(0.95))</p>
<h1 id="categorical-data-handling">3. Categorical Data Handling</h1>
<h1 id="convert-sex-and-embarked-into-numerical-values-using-one-hot-encoding">Convert ‘Sex’ and ‘Embarked’ into numerical values using one-hot encoding</h1>
<p>df = pd.get_dummies(df, columns=[‘Sex’, ‘Embarked’])</p>
<h1 id="create-new-features-by-parsing-name-to-extract-titles">Create new features by parsing ‘Name’ to extract titles</h1>
<p>df[‘Title’] = df[‘Name’].str.extract(’ ([A-Za-z]+).’, expand=False)</p>
<h1 id="descriptive-statistics">4. Descriptive Statistics</h1>
<h1 id="generate-summary-statistics">Generate summary statistics</h1>
<p>summary_stats = df.describe()<br>
frequency_counts = df[‘Embarked’].value_counts()</p>
<h1 id="data-visualization">5. Data Visualization</h1>
<h1 id="create-histograms-and-boxplots">Create histograms and boxplots</h1>
<p>df[‘Age’].hist(bins=20)<br>
df.boxplot(column=‘Fare’, by=‘Pclass’)</p>
<h1 id="develop-bar-charts">Develop bar charts</h1>
<p>df[‘Sex’].value_counts().plot(kind=‘bar’)<br>
df[‘Embarked’].value_counts().plot(kind=‘bar’)</p>
<h1 id="plot-survival-rates-against-various-factors">Plot survival rates against various factors</h1>
<p>survival_rates = df.groupby(‘Pclass’)[‘Survived’].mean()<br>
survival_rates.plot(kind=‘bar’)</p>
<h1 id="correlation-analysis">6. Correlation Analysis</h1>
<h1 id="calculate-correlation-matrix">Calculate correlation matrix</h1>
<p>correlation_matrix = df.corr()</p>

