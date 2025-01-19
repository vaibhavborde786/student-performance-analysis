import pandas as pd
import numpy as np

# Load data
data = pd.read_csv('student_performance.csv')

# Inspect schema and summary
print(data.info())
print(data.describe())

# Handle missing values
data = data.dropna()

# Identify patterns: performance by topic and difficulty
performance_by_topic = data.groupby('Topic')['Accuracy'].mean()
performance_by_difficulty = data.groupby('Difficulty')['Accuracy'].mean()

# Visualize
import matplotlib.pyplot as plt
performance_by_topic.plot(kind='bar')
plt.title('Performance by Topic')
plt.show()

