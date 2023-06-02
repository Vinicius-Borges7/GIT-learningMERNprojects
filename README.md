# IF4Health Site Management
My first task as a scholarship holder from Ifsul's research group called If4Health was to transform a static website into a dynamic MERN web app. The website was created by https://github.com/andredelmestre, and he also developed a prototype for the backend, upon which my changes are based.

This repository represents the backend of the application, obviously.

## How to Run
---
### Dependencies
first, install the dependencies
````powershell
npm install
````

### AWS S3 Bucket and IAM
So, create a account on AWS if you dont have one and do a S3 Bucket for you, this process is to complex to explain here so good luck. 
You need to create two users on AWS IAM too, they are "common users" and "adm"(both could be another name). all users need a data access policy, I will give you a template to just run the app here:

Adm's policy:
````JSON
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "AllowReadWriteDelete",
            "Effect": "Allow",
            "Action": [
                "s3:GetObject",
                "s3:PutObject",
                "s3:DeleteObject",
                "s3:ListBucket"
            ],
            "Resource": [
                "arn:aws:s3:::YOUR_S3_BUCKET_NAME/*",
                "arn:aws:s3:::YOUR_S3_BUCKET_NAME"
            ]
        }
    ]
}
````

Common User's Policy:
````JSON
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "s3:GetObject"
            ],
            "Resource": [
                "arn:aws:s3:::YOUR_S3_BUCKET_NAME/*"
            ]
        }
    ]
}
````
### Enviroment
then with AWS things done, now you need to fill the enviroment variables with your data
| Variable                | Description                                                |
|-------------------------|------------------------------------------------------------|
| PORT                    | The port who the server must run                           |
| DB_NAME                 | Name from your mongodb database                            |
| DB_URI                  | URL from your atlas cluster/database                       |
| BUCKET_NAME             | Name from your AWS S3 Bucket                               |
| BUCKET_REGION           | Location where your bucket is hosted                       |
| ADM_ACESS_KEY           | Acess key from your ADM user(AWS IAM)                      |
| ADM_SECRET_KEY          | Secret key from your ADM user(AWS IAM)                     |

### Start Commands  
to start the server, use the command          
````powershell
npm start
````        

## Routes
with everthing running, these are the routes
| Route                   | Method | Description                                                |
|-------------------------|--------|------------------------------------------------------------|
| `/`                     | GET    | Go to home page.                                           |
| `/students`             | GET    | Go to students interface.                                  |
| `/students/data`        | GET    | Get all students                                           |
| `/students/:id`         | GET    | Get one student.                                           |
| `/students/myForm`      | POST   | Register one student on db.                                |
| `/students/update/:id`  | PUT    | Upload a student status.                                   |
| `/students/delete/:id`  | DELETE | Delete a student.                                          |
| `/works`                | GET    | Go to the works interface.                                 |
| `/works/data`           | GET    | Get all works.                                             |
| `/works/:id`            | GET    | Get one work.                                              |
| `/works/myForm`         | POST   | Register one work on DB.                                   |
| `/works/delete/:id`     | DELETE | Delete a work.                                             |
| `/projects`             | GET    | Go to the projects interface.                              |
| `/projects/data`        | GET    | Get all projects.                                          |
| `/projects/:id`         | GET    | Get one project.                                           |
| `/projects/myForm`      | POST   | Register a Project.                                        |
| `/projects/delete/:id`  | DELETE | Delete a project.                                          |
| `/linkTrees`            | GET    | Go to the link trees interface.                            |
| `/linkTrees/data`       | GET    | Get all link trees.                                        |
| `/linkTrees/single/:id` | GET    | Get one link tree.                                         |
| `/linkTrees/myForm`     | POST   | Register one link tree on db.                              |
| `/linkTrees/delete/:id` | DELETE | Delete a link tree.                                        |
