# Working with DVC (Data Version Control)

```dvc init```

```dvc add data/custom_data.csv```
---

# To get the older version data use the below command
## Fistly checkout to the git version
```git checkout <hash_value>```

## Then hit the command
```dvc checkout```

dvc will look for the data that has the hash value present in custom_data.csv.dvc