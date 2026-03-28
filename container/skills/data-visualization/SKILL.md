---
name: data-visualization
description: Create professional charts and graphs using matplotlib and seaborn. Use this to turn raw data (from CSV, JSON, or Excel) into visual insights.
---

# Data Visualization Skill

This skill enables the creation of professional, publication-ready charts and graphs using Python's `matplotlib` and `seaborn` libraries.

## Dependencies
Ensure these are installed in the environment:
```bash
pip install matplotlib seaborn pandas
```

## Guidelines
1. **Always save to file**: Do not use `plt.show()` in headless environments. Always use `plt.savefig('filename.png')`.
2. **Use Seaborn for aesthetics**: Seaborn provides better default styles than base matplotlib.
3. **Clear labels**: Always include a title, x-label, and y-label.
4. **Handle Chinese characters**: If the data contains Chinese, ensure a CJK font is set (e.g., `plt.rcParams['font.sans-serif'] = ['Noto Sans CJK JP']`).

## Example: Bar Chart from Data

```python
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns

# 1. Set style
sns.set_theme(style="whitegrid")

# 2. Prepare data
data = {
    'Month': ['Jan', 'Feb', 'Mar', 'Apr', 'May'],
    'Sales': [1500, 2300, 1800, 3200, 2800]
}
df = pd.DataFrame(data)

# 3. Create plot
plt.figure(figsize=(10, 6))
ax = sns.barplot(x='Month', y='Sales', data=df, palette='viridis')

# 4. Customize
plt.title('Monthly Sales Performance', fontsize=16, pad=15)
plt.xlabel('Month', fontsize=12)
plt.ylabel('Sales ($)', fontsize=12)

# Add value labels on top of bars
for i in ax.containers:
    ax.bar_label(i, padding=3)

# 5. Save and close
plt.tight_layout()
plt.savefig('sales_chart.png', dpi=300)
plt.close()
```
