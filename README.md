### EX3 Implementation of GSP Algorithm In Python
### DATE: 12.04.25
### AIM: To implement GSP Algorithm In Python.
### Description:
The Generalized Sequential Pattern (GSP) algorithm is a data mining technique used for discovering frequent patterns within a sequence database. It operates by identifying sequences that frequently occur together. GSP works by employing a depth-first search strategy to explore and extract frequent patterns efficiently.
### Steps:
1. <strong>Database Scanning:</strong> GSP scans the sequence database to determine the support of each item in the dataset.
2. <strong>Candidate Generation:</strong> It generates a set of candidate sequences using frequent items found in the previous step.
3. <strong>Pattern Growth:</strong> It extends the candidate sequences by merging them to form longer patterns, checking their support against a user-defined minimum support threshold.
4. <strong>Repeat:</strong> The process continues until no new sequences meet the minimum support threshold.
<p align="justify">
GSP finds application in various domains such as market basket analysis, web usage mining, bioinformatics, and more. For instance, in retail, GSP can identify common purchasing patterns, helping businesses understand customer behavior for targeted marketing or inventory management.
</p>

### Procedure:
<p align="justify">
1. From collections import defaultdict, from itertools import combinations: Imports necessary libraries/modules. defaultdict is
used to create a dictionary with default values and combinations generates all possible combinations of a sequence.</p>
<p align="justify">
2. generate_candidates(dataset, k): Function to generate candidate k-item sequences from a dataset. It loops through each sequence in the
dataset and finds combinations of length k for each sequence, updating their counts in a dictionary.</p>
<p align="justify">
3. gsp(dataset, min_support): Function that implements the Generalized Sequential Pattern (GSP) algorithm. It iterates through increasing
sequence lengths (k) until no new frequent patterns are found. It calls generate_candidates() to find patterns of varying lengths.</p>
<p align="justify">
4. Example dataset for each category: Defines example sequences for top wear, bottom wear, and party wear categories.</p>
<p align="justify">
5. Minimum support threshold: Sets the minimum support count required for a pattern to be considered frequent.</p>
<p align="justify">
6. Perform GSP algorithm for each category: Applies the GSP algorithm for each category using the defined example datasets and the
minimum support threshold.</p>
<p align="justify">
7. Output the frequent sequential patterns for each category: Prints the frequent sequential patterns 
    along with their support counts
for each wear category.</p>
<p align="justify">
8. Visulaize the sequence patterns using matplotlib.
</p>
## Program:

```python
from collections import defaultdict
from itertools import combinations
from tabulate import tabulate  # Import tabulate library

# Function to generate candidate k-item sequences
def generate_candidates(dataset, k):
    candidates = defaultdict(int)
    for sequence in dataset:
        for itemset in combinations(sequence, k):
            candidates[itemset] += 1
    return {item: support for item, support in candidates.items() if support >= min_support}

# Function to perform GSP algorithm
def gsp(dataset, min_support):
    frequent_pattern_1_item = defaultdict(int)
    frequent_pattern_multi_item = defaultdict(int)
    k = 1
    sequence = dataset
    while True:
        candidates = generate_candidates(sequence, k)
        if not candidates:
            break
        if k == 1:
            frequent_pattern_1_item.update(candidates)
        else:
            frequent_pattern_multi_item.update(candidates)
        k += 1
    return frequent_pattern_1_item, frequent_pattern_multi_item

# Example dataset for each category
top_wear_data = [
    ["blouse", "t-shirt", "tank_top"],
    ["hoodie", "sweater", "top"], 
    ["hoodie"], 
    ["hoodie", "sweater"]
]
bottom_wear_data = [
    ["jeans", "trousers", "shorts"],
    ["leggings", "skirt", "chinos"]
]
party_wear_data = [
    ["cocktail_dress", "evening_gown", "blazer"],
    ["party_dress", "formal_dress", "suit"],
    ["party_dress", "formal_dress", "suit"],
    ["party_dress", "formal_dress", "suit"],
    ["party_dress", "formal_dress", "suit"],
    ["party_dress"], 
    ["party_dress"]
]
# Minimum support threshold
min_support = 2

# Perform GSP algorithm for each category
top_wear_1_item_result, top_wear_multi_item_result = gsp(top_wear_data, min_support)
bottom_wear_1_item_result, bottom_wear_multi_item_result = gsp(bottom_wear_data, min_support)
party_wear_1_item_result, party_wear_multi_item_result = gsp(party_wear_data, min_support)

# Function to format the results into a table
def format_table(results, category, is_multi_item=False):
    if results:
        table = [[str(pattern), support] for pattern, support in results.items()]
        headers = ["Pattern", "Support"]
        table_type = "Multi-Item" if is_multi_item else "1-Item"
        return f"\nFrequent Sequential Patterns - {category} ({table_type} Sequences):\n" + tabulate(table, headers, tablefmt="grid")
    else:
        return f"\nNo frequent sequential patterns found in {category} ({'Multi-Item' if is_multi_item else '1-Item'} Sequences).\n"

# Output the frequent sequential patterns for each category in tabular form
print(format_table(top_wear_1_item_result, "Top Wear"))
print(format_table(top_wear_multi_item_result, "Top Wear", is_multi_item=True))

print(format_table(bottom_wear_1_item_result, "Bottom Wear"))
print(format_table(bottom_wear_multi_item_result, "Bottom Wear", is_multi_item=True))

print(format_table(party_wear_1_item_result, "Party Wear"))
print(format_table(party_wear_multi_item_result, "Party Wear", is_multi_item=True))
```


## Visualization:
```python
import matplotlib.pyplot as plt

# Function to visualize frequent sequential patterns with a line plot
def visualize_patterns_line(result, category):
    if result:
        patterns = list(result.keys())
        support = list(result.values())

        plt.figure(figsize=(10, 6))
        plt.plot([str(pattern) for pattern in patterns], support, marker='o', linestyle='-', color='blue')
        plt.xlabel('Patterns')
        plt.ylabel('Support Count')
        plt.title(f'Frequent Sequential Patterns - {category}')
        plt.xticks(rotation=90)
        plt.tight_layout()
        plt.show()
    else:
        print(f"No frequent sequential patterns found in {category}.")

# Visualize frequent sequential patterns for each category using a line plot
visualize_patterns_line(top_wear_result, 'Top Wear')
visualize_patterns_line(bottom_wear_result, 'Bottom Wear')
visualize_patterns_line(party_wear_result,'Party Wear')

```
## Output:

![image](https://github.com/user-attachments/assets/d1a627a1-b088-475f-8049-957408a91167)
### Visualization:
![image](https://github.com/user-attachments/assets/cd9e9840-a6df-4895-9756-9e20a98fbbff)
![image](https://github.com/user-attachments/assets/f1676eab-cb21-4775-b557-4473aa570281)

## Result:
Thus the implementation of the GSP algorithm in python has been successfully executed.
