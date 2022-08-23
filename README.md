# SQLite Docker 

Christopher Glenn  
chglenn20@gmail.com

## About

An attempt at a pseudo-stateful app container via Docker volumes and sqlite3.

**DISCLAIMER:** I am not the first person to do this. My implementation is very bare-bones and is by no means original. This project is for education only and should not be used in a production environment. I provide no warranty or support for external use of this project. Please use at your own risk. 

## Usage

### Pull the image
`docker pull chglenn20/sqlite-docker:latest`

### Starting the database
`docker run -it -v ~/db:/db chglenn20/sqlite-docker database.db`

- `-it` Interactive to allow shell, pseudo-tty  
- `-v ~/db:/db` Mount local volume `~/db` to container volume `/db`  
- `database.db` Entry command to assign database output file name.  

Once you've ran the image, you're ready to start running commands against your database. Check out [the SQLite docs](https://sqlite.org/cli.html) for some helpful commands. Once you've run your first command, your database can be found on your local machine at `~/db/database.db`. 

### Dumping the database
`docker run -it -v ~/db:/db chglenn20/sqlite-docker database.db .dump >> dump.sql`  

This will create a `dump.sql` file in this project folder which can be used as a backup.

### Restoring the database
`mv ~/db/database.db ~/db/database.db.old`  
`cat dump.sql | docker run -it -v ~/db:/db chglenn20/sqlite-docker database.db`

This will rename the existing database and restore the last backup (dump.sql) to the database. 
