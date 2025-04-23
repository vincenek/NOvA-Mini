git checkout -b feature/navigation
# Edit index.html to add navigation links
git add index.html
git commit -m "Add navigation to all sections"
git checkout main
git merge feature/navigation