# Ultimate Matplotlib, Pyplot & Seaborn Cheat Sheet

> **The most complete, thoroughly researched, and beautifully organized reference guide for Python data visualization.**
> 
> Covers Matplotlib 3.10+, Seaborn 0.13+ | 2026 Edition | 34,000+ words | 16 sections | 100+ functions
---

## Table of Contents

- [Overview](#overview)
- [What's Included](#whats-included)
- [Quick Start](#quick-start)
- [Cheat Sheet Sections](#cheat-sheet-sections)
- [Visual Diagrams](#visual-diagrams)
- [Matplotlib vs Seaborn Comparison](#matplotlib-vs-seaborn-comparison)
- [Installation](#installation)
- [Usage Examples](#usage-examples)
- [SEO Keywords](#seo-keywords)
- [Contributing](#contributing)
- [License](#license)
- [Acknowledgments](#acknowledgments)

---

## Overview

This repository contains the **ultimate cheat sheet** for Python data visualization using **Matplotlib**, **Matplotlib.pyplot**, and **Seaborn**. Whether you're a beginner learning your first plots or an experienced data scientist looking for a quick reference, this guide has you covered.

**Key Features:**
- 100+ functions documented with syntax, parameters, and real examples
- Clean markdown tables that render perfectly on GitHub, VS Code, Jupyter, and any markdown viewer
- Visual hierarchy diagrams showing function relationships
- Complete mapping between Matplotlib and Seaborn equivalents
- 2026 edition - updated for the latest library versions

---

## What's Included

### 1. Master Cheat Sheet (`Ultimate_Matplotlib_Seaborn_CheatSheet.md`)

A comprehensive 34,000+ character reference covering:

| Category | Functions Covered |
|----------|-------------------|
| **Import & Setup** | `import matplotlib`, `import seaborn`, `set_theme`, `style.use`, `rcParams` |
| **Basic Plotting** | `plot`, `scatter`, `bar`, `hist`, `boxplot`, `pie`, `fill_between`, `stackplot`, `step`, `errorbar`, `stem`, `violinplot`, `polar`, `loglog`, `eventplot` |
| **Customization** | `title`, `xlabel`, `ylabel`, `legend`, `grid`, `xticks`, `yticks`, `xlim`, `ylim`, `axis`, `tick_params`, `spines`, `colorbar`, `margins`, `autoscale` |
| **Grid & Layout** | `figure`, `subplots`, `subplot`, `subplot_mosaic`, `GridSpec`, `tight_layout`, `constrained_layout`, `twinx`, `twiny` |
| **Text & Annotations** | `text`, `annotate`, `arrow`, `axvline`, `axhline`, `axvspan`, `axhspan`, `axline`, `table`, math text |
| **Advanced Features** | `contour`, `imshow`, `pcolormesh`, `quiver`, `streamplot`, `hexbin`, `specgram`, `3D projection` |
| **Output & Saving** | `show`, `savefig`, `clf`, `cla`, `close`, `draw`, `pause`, event handling |
| **Seaborn Figure-Level** | `relplot`, `displot`, `catplot` with full parameter documentation |
| **Seaborn Relational** | `scatterplot`, `lineplot` |
| **Seaborn Distribution** | `histplot`, `kdeplot`, `ecdfplot`, `rugplot` |
| **Seaborn Categorical** | `stripplot`, `swarmplot`, `boxplot`, `violinplot`, `boxenplot`, `pointplot`, `barplot`, `countplot` |
| **Seaborn Regression** | `regplot`, `lmplot`, `residplot` |
| **Seaborn Matrix** | `heatmap`, `clustermap` |
| **Seaborn Multi-Plot** | `FacetGrid`, `PairGrid`, `pairplot`, `JointGrid`, `jointplot` |
| **Seaborn Themes** | `set_theme`, `set_style`, `set_context`, `set_palette`, color palette generators |
| **Quick Reference** | Complete Matplotlib to Seaborn function mapping table |

### 2. Visual Diagrams

- **Function Hierarchy Diagram** - Shows Seaborn's figure-level vs axes-level architecture
- **Function Mapping Reference** - Side-by-side comparison of Matplotlib vs Seaborn equivalents
- **Styling Parameters Guide** - Color palettes, markers, line styles, and universal parameters

---

## Quick Start

```python
# Standard imports
import matplotlib.pyplot as plt
import seaborn as sns
import numpy as np
import pandas as pd

# Set theme
sns.set_theme(style='whitegrid', palette='pastel')

# Quick example
fig, ax = plt.subplots(figsize=(10, 6))
sns.scatterplot(data=df, x='x_column', y='y_column', hue='category', ax=ax)
plt.title('My Plot')
plt.tight_layout()
plt.savefig('output.png', dpi=300, bbox_inches='tight')
plt.show()
```

---

## Cheat Sheet Sections

### Section 1: Import & Setup
Learn how to import libraries, set themes, configure backends, and apply style sheets.

### Section 2-7: Matplotlib.pyplot
Complete coverage of pyplot functions organized by category:
- Basic plotting functions
- Customization and styling
- Grid layout and subplots
- Text, annotations, and arrows
- Advanced features (contours, vectors, 3D)
- Output, saving, and event handling

### Section 8-15: Seaborn
Comprehensive Seaborn documentation:
- Figure-level vs axes-level function architecture
- Relational, distribution, and categorical plots
- Regression and matrix plots
- Multi-plot grids (FacetGrid, PairGrid, JointGrid)
- Themes, contexts, and color palettes

### Section 16: Quick Reference
Complete mapping table showing which Matplotlib function corresponds to which Seaborn function.

---

## Visual Diagrams

### Seaborn Function Hierarchy
![Function Hierarchy](images/seaborn_matplotlib_hierarchy.png)

Shows how Seaborn's figure-level functions (`relplot`, `displot`, `catplot`) relate to their underlying axes-level functions and Matplotlib.

### Function Mapping Reference
![Function Mapping](images/function_mapping_reference.png)

Quick-reference table mapping 20+ visualization types between Matplotlib and Seaborn (both axes-level and figure-level).

---

## Matplotlib vs Seaborn Comparison

| Feature | Matplotlib | Seaborn |
|---------|------------|---------|
| **Level** | Low-level, highly customizable | High-level, statistical visualization |
| **API Style** | Object-oriented and pyplot | DataFrame-aware, declarative |
| **Best For** | Fine-grained control, publication plots | Statistical analysis, quick EDA |
| **Data Input** | Arrays and lists | Pandas DataFrames preferred |
| **Styling** | Manual configuration | Built-in themes and palettes |
| **Faceting** | Manual subplot creation | Built-in `col` and `row` parameters |
| **Integration** | Foundation for all Python plotting | Built on top of Matplotlib |

**Pro Tip:** Use Seaborn for exploration and statistical plots, then drop down to Matplotlib for fine-tuning and publication-ready figures.

---

## Installation

```bash
# Install required packages
pip install matplotlib seaborn pandas numpy

# For Jupyter notebooks
pip install jupyter

# Optional: for interactive plots
pip install ipympl
```

### Version Requirements
- Python >= 3.9
- Matplotlib >= 3.10
- Seaborn >= 0.13
- Pandas >= 1.5
- NumPy >= 1.21

---

## Usage Examples

### Example 1: Basic Line Plot
```python
import matplotlib.pyplot as plt
import numpy as np

x = np.linspace(0, 10, 100)
y = np.sin(x)

plt.plot(x, y, 'b-', linewidth=2, label='sin(x)')
plt.title('Sine Wave')
plt.xlabel('x')
plt.ylabel('sin(x)')
plt.legend()
plt.grid(True, alpha=0.3)
plt.show()
```

### Example 2: Seaborn Statistical Plot
```python
import seaborn as sns
import matplotlib.pyplot as plt

# Load sample data
tips = sns.load_dataset('tips')

# Create figure-level plot with faceting
g = sns.relplot(
    data=tips, x='total_bill', y='tip',
    hue='smoker', col='time', row='sex',
    kind='scatter', height=4, aspect=1.2
)
g.set_axis_labels('Total Bill ($)', 'Tip ($)')
g.set_titles(col_template='{col_name}', row_template='{row_name}')
plt.show()
```

### Example 3: Heatmap with Annotations
```python
import seaborn as sns
import matplotlib.pyplot as plt
import numpy as np

# Create correlation matrix
data = np.random.randn(10, 10)
corr = np.corrcoef(data)

plt.figure(figsize=(10, 8))
sns.heatmap(
    corr, annot=True, fmt='.2f',
    cmap='coolwarm', center=0,
    square=True, linewidths=0.5,
    cbar_kws={'shrink': 0.8}
)
plt.title('Correlation Matrix')
plt.tight_layout()
plt.show()
```

---

## SEO Keywords

**Primary Keywords:**
- matplotlib cheat sheet
- seaborn cheat sheet
- python data visualization
- matplotlib.pyplot reference
- seaborn tutorial

**Secondary Keywords:**
- python plotting guide
- matplotlib functions list
- seaborn functions complete
- data visualization python
- matplotlib vs seaborn
- seaborn figure level vs axes level
- matplotlib subplot tutorial
- seaborn heatmap tutorial
- python statistical visualization
- matplotlib savefig dpi

**Long-tail Keywords:**
- complete matplotlib seaborn reference guide
- matplotlib pyplot all functions explained
- seaborn relplot displot catplot tutorial
- how to use seaborn with matplotlib
- python visualization cheat sheet 2026
- seaborn color palette guide
- matplotlib annotation examples
- seaborn facetgrid tutorial

---

## Contributing

Contributions are welcome! If you find errors, want to add examples, or suggest improvements:

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-improvement`)
3. Commit your changes (`git commit -m 'Add amazing improvement'`)
4. Push to the branch (`git push origin feature/amazing-improvement`)
5. Open a Pull Request

Please ensure your contributions follow the existing format and include working code examples.

---

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

---

## Acknowledgments

- **Matplotlib Team** for the foundational plotting library
- **Seaborn Team** for the statistical visualization interface
- **Python Data Science Community** for continuous improvements and best practices
- Inspired by official documentation, RealPython tutorials, and CodeAcademy guides

---

## Related Resources

- [Matplotlib Official Documentation](https://matplotlib.org/stable/contents.html)
- [Seaborn Official Documentation](https://seaborn.pydata.org/tutorial.html)
- [RealPython Matplotlib Guide](https://realpython.com/python-matplotlib-guide/)
- [Pandas Visualization](https://pandas.pydata.org/docs/user_guide/visualization.html)
- [Python Graph Gallery](https://www.python-graph-gallery.com/)

---

