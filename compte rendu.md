# ZINEB EL MEJDOUBI
**Numéro d'étudiant** : 24010156
**Classe** : CAC2


# Compte rendu

📊## Analyse de l'Équilibre entre Usage des Réseaux Sociaux et Santé Mentale 

**Date :** 29 Novembre 2025

import re

toc_lines = []

for line in readme_content.split('\n'):
    if line.strip().startswith('#'):
        # Extract the level (number of #) and the title text
        match = re.match(r'^(#+)\s*(.*)$', line)
        if match:
            level = len(match.group(1))
            title = match.group(2).strip()
            # Format the title for the link (lowercase, replace spaces with hyphens, remove special characters)
            anchor = title.lower().replace(' ', '-').replace('(', '').replace(')', '').replace('.', '').replace(',', '').replace(':', '').replace('`', '')
            # Create indentation based on level
            indentation = '  ' * (level - 1)
            toc_lines.append(f"{indentation}- [{title}](#{anchor})")

# Display the Table of Contents
print("## Table des Matières\n")
for entry in toc_lines:
    print(entry)

print("\n---\n") # Separator

# Display the full README content
print(readme_content)

