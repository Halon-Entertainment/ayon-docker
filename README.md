ayon-docker
===========

Make a file in /postgres-init/init-db.sql with the following content:

- Replace `ayon` with your desired password

```
DO $$
BEGIN
    -- Check if role 'ayon' already exists
    IF NOT EXISTS (SELECT 1 FROM pg_roles WHERE rolname = 'ayon') THEN
        -- Create role 'ayon' if it doesn't exist
        CREATE ROLE ayon WITH LOGIN PASSWORD 'ayon';
        ALTER ROLE ayon CREATEDB;
    END IF;

    -- Check if database 'ayon' already exists
    IF NOT EXISTS (SELECT 1 FROM pg_database WHERE datname = 'ayon') THEN
        -- Create database 'ayon' if it doesn't exist
        CREATE DATABASE ayon OWNER ayon;
    END IF;
END $$;
```

*WINDOWS*

1. Clone ayon-docker repository to your local machine.
2. Tweak the docker-compose.yml file according to your requirements.
3. You may use the .env file to set environment variables.
4. Comment-out or delete the - "/etc/localtime:/etc/localtime:ro" line from the docker-compose.yml file.
5. Run the stack using docker compose up -d
6. Run manage.ps1 setup to set up the server. If you get a permission error, you may need to set your execution policy to RemoteSigned by running Set-ExecutionPolicy RemoteSigned in PowerShell stackoverflow.
7. Once the setup is complete, navigate to http://localhost:5000/ in your web browser and log in as admin/admin.

*LINUX*
1. Clone ayon-docker repository to the machine.
2. Tweak the docker-compose.yml file according to your requirements.
3. You may use the .env file to set environment variables.
5. Run the stack using docker compose up -d
6. Run make setup
7. Once the setup is complete, navigate to http://localhost:5000/
8. Log in as admin/admin.