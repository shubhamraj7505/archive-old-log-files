# Archive-old-log-files-Project


Suppose if a application of linux server/local server produces log file
of 10GB, 20GB or more. After some time disk will be full or out of space
by these log files.<br>
So, we have to compress these file by E.O.D

### Steps:
- Provide the path of directory in which you want to perform action.
```sh
    BASE=/home/piyush/Downloads/log_files
```

- Check if directory is present or not.
```sh
    if [ ! -d $BASE ]
    then
        echo "directory does not exist: $BASE"
        exit 1
    fi
```

- Create 'archive' directory at that location($BASE) if not already present
```sh
    if [ ! -d $BASE/archive ]
    then
        mkdir $BASE/archive
    fi
```

- Find all the files with size more than 10GB or any size you want.
```sh
    for i in `find $BASE -maxdepth $DEPTH -type f -size +10M`
```

- If found, then compress each file.
```sh
    gzip $i || exit 1
```

- Move the compressed files in 'archive' directory.
```sh 
    mv $i.gz $BASE/archive || exit 1
```

- Make a cron job to execute the scripts every day at given time.(At 20:00 Hrs)
```sh
    00 20 * * * /home/piyush/user/91705/Archive-old-log-files-Project/archive_project.sh
```
