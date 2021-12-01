# hasura-spring-boot-starter
A starter kit for Hasura + Java Spring boot for building a GraphQL API with remote/logical fields
powered by business logic in Java.

## Getting started

- Run a docker build command: `docker build -t .`
- Run with docker: `docker-compose up -d`


## Run the demo

- Build the docker image and run it
- Open the Hasura console at `http://localhost:8080`
- Create the sample database
  - `docker run -ti postgres < psql < ./demo/data.sql`
- Import the sample metadata Hasura Console > Data > Run SQL
  - Hasura Console > Setings > Import metadata > `./demo/metadata.json`
- Try the following GraphQL query:
```
query {
  user {
    id
    email
    age
  }
}
```
- Here, you'll see that the user model is the base model and age is a computed field
  and the logic is powered by code in Java

## Usage notes & tutorial

1. Set up or use an existing database as a data source
2. Track a data model via the Hasura metadata in the metadata directory
3. Add a resolver that represents a new field to the Java spring boot app ([howto](#add-field-java-spring-boot))
4. Build the docker image and run it [howto](#getting-started)
  - The docker image build process will automatically build the Java API
  - Tip: Run docker-compose in `watch` mode if you don't want to rebuild the docker image every time as you're developing!
5. Now use either the CLI or the console to:
  - Add the java spring boot GraphQL API as a remote schema - `http://localhost:3000`
  - Add the remote field to the data model as a remote relationship [howto]()
  - If you're using the CLI, remember to run a `hasura metadata apply` after you modify the metadata
  - If you're using the console remember to run a `hasura metadata export` after you modify the metadata via the console, so that your latest metadata is exported as code in your metadata directory
7. Test out the GraphQL API

## Deploying in production

1. For deploying in production, once you're done with development, build the docker image and name/tag it appropriately
2. Use the built docker image when running Hasura instead of using hasura/graphql-engine directly
3. Make sure you have your metadata database and your source database already running and set up
4. Once you have the container running, apply your metadata using:
  - `hasura metadata apply`
