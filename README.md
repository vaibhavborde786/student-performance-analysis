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
===================================
# Identify weak areas (accuracy below threshold)
weak_areas = performance_by_topic[performance_by_topic < 0.6]

# Recommend improvement areas
recommended_topics = weak_areas.index.tolist()

# Create student persona
if weak_areas.any():
    persona = "Needs Focus on Specific Topics"
else:
    persona = "Well-rounded Learner"

print(f"Persona: {persona}")
print(f"Recommended Topics for Improvement: {recommended_topics}")

