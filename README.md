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
To begin, create an account on AWS if you don't have one and set up an S3 Bucket. The process of creating a bucket is complex to explain here, so good luck.
You also need to create two users in AWS IAM: one for common users and another for administrative tasks. You can name them whatever you prefer. All users require a data access policy. Below is a template for running the app:

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
| Variable                | Description                                                         |
|-------------------------|---------------------------------------------------------------------|
| PORT                    | The port on which the server must run.                              |
| DB_NAME                 | Name from your MongoDB database.                                    |
| DB_URI                  | URL of your Atlas cluster/database.                                 |
| BUCKET_NAME             | Name of your AWS S3 Bucket.                                         |
| BUCKET_REGION           | Location where your bucket is hosted.                               |
| ADM_ACESS_KEY           | Acess key of your ADM user(AWS IAM).                                |
| ADM_SECRET_KEY          | Secret key of your ADM user(AWS IAM).                               |

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
| `/students/:id`         | GET    | Get a single student.                                      |
| `/students/myForm`      | POST   | Register a single student on db.                           |
| `/students/update/:id`  | PUT    | Upload a student status.                                   |
| `/students/delete/:id`  | DELETE | Delete a single student.                                   |
| `/works`                | GET    | Go to the works interface.                                 |
| `/works/data`           | GET    | Get all works.                                             |
| `/works/:id`            | GET    | Get a single work.                                         |
| `/works/myForm`         | POST   | Register a single work on DB.                              |
| `/works/delete/:id`     | DELETE | Delete a single work.                                      |
| `/projects`             | GET    | Go to the projects interface.                              |
| `/projects/data`        | GET    | Get all projects.                                          |
| `/projects/:id`         | GET    | Get a single project.                                      |
| `/projects/myForm`      | POST   | Register a Project.                                        |
| `/projects/delete/:id`  | DELETE | Delete a single project.                                   |
| `/linkTrees`            | GET    | Go to the link trees interface.                            |
| `/linkTrees/data`       | GET    | Get all link trees.                                        |
| `/linkTrees/single/:id` | GET    | Get a single link tree.                                    |
| `/linkTrees/myForm`     | POST   | Register a single link tree on db.                         |
| `/linkTrees/delete/:id` | DELETE | Delete a link tree.                                        |
