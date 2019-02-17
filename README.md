# Simple Dockerised Postgres instance #

## Purpose ##

I made this project as part of a [very basic tutorial](https://hackerbox.io/articles/postgres-docker-setup/) on how to run Postgres inside a Docker container.

Database setup is achieved using a script that is first passed into the Postgres container using a volume.

**NOTE: this project has only been tested on OSX.**

## Instructions ##

### Run the container ###

Navigate to the project root, and start the container with the following command:

```bash
docker run --name hackerbox-postgres-test -v $(pwd)/scripts:/scripts --env-file ./.env -p 5432:5432 -d postgres:11.1
```

Run the setup script:

```bash
docker exec hackerbox-postgres-test bash -c 'psql -U postgres -f ./scripts/setup.psql'
```

### Check that the data is present ###

Connect to the container:

```bash
docker exec -it hackerbox-postgres-test bash
```

Connect to the database:

```bash
\c hackerbox_test_db
```

NOTE: you should receive a verification similar to the following:

```text
You are now connected to database "hackerbox_test_db" as user "postgres".
```

Query the **people** table:

```bash
select * from people;
```

You should now see the contents of the **people** table:

```text
 id | forename | surname
----+----------+---------
  1 | Alan     | Turing
(1 row)
```

## Additional info ##

The database name and password are set in the **.env** file, so have a look in there before you attempt to connect to the running container externally.