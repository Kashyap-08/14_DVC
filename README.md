# Working with DVC (Data Version Control)

```dvc init```

```dvc add data/custom_data.csv```

# To get the older version data use the below command

## Fistly checkout to the git version 
```git checkout <hash_value>```

## Then hit the command
```dvc checkout```


##### dvc will look for the data that has the hash value present in custom_data.csv.dvc

# To upload files to s3

```create s3 bucket```

```
create iam user  
1. give user name  
2. hit next and select attach policy directly  
3. select s3fillAccess from permission policy  
4. get inside created user and get into security credentials  
5. scroll below to create access key  
6. select other  
7. and hit create access key buttion  
8. you will get the access key and secret access key.
9. store those creds and also the region
```


```
s3 = boto3.resource(
    service_name='s3',
    region_name='us-east-1',
    aws_access_key_id='AKIA4EHEUOD2JJR7CMUW',
    aws_secret_access_key='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'
)
```


```
bucket = 'k-dvc-bucket'
file_path = os.path.join(os.getcwd(), 'data','custom_data.csv')
print(file_path)
```

```
s3.Bucket(bucket).upload_file(Filename = file_path, Key = 'sampe_file.csv')
```

# Configure dvc to store dvc version files to s3
Step1: Get into s3 bucket and crate folder.
Step2: Get into folder and copy s3 url
```
s3://k-dvc-bucket/dvc_store/
```

step3: Install 
```
pip install dvc[s3]
```

step4: configure aws credentials using command
```
export AWS_ACCESS_KEY_ID=your-access-key-id
export AWS_SECRET_ACCESS_KEY=your-secret-access-key
export AWS_DEFAULT_REGION=your-region
```

step5: set remote repository for dvc
```
dvc remote add -d myremote s3://k-dvc-bucket/dvc_store/
```

step6: Push the files
```
dvc push
```