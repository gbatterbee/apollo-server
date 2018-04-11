---

title: Getting started

---

## Overview
> Estimated time: About 10 minutes.

In this guide, we'll walk you through the process of creating a GraphQL server in JavaScript.  By the end of the guide you should expect to:

* Have a basic GraphQL server which will work as a foundation for a more complex server.
* Have a basic understanding of the fundamental GraphQL principles.
* Be able to send a query to the new GraphQL server and see the response using the GraphiQL user interface.

If you want to skip walking through the steps, the "More information" section at the bottom has a link to a GitHub repository which can be cloned and ran locally.

## Prerequisites

* Familiarity with JavaScript. ([Getting started with JavaScript]())
* Terminal/console access on your computer. ([Popular terminals]())
* Node.js (`node`) and its package manager (`npm`) installed. ([Node.js]())
* An editor or interactive developer environment (IDE) to create and modify files. ([Popular IDEs]())
* The desire to build a GraphQL server. ([Why GraphQL?]())

If you don't meet any of the prerequisites above, we recommend following the links we've provided  aside each item and returning to this guide once you're ready.

## Step 1: Project initialization

In this step, we'll use your terminal (e.g. Terminal, iTerm, PowerShell) to create a directory called `graphql-server-example` along with a basic Node.js configuration for a simple application.  We'll work within this directory for the rest of the steps, though we will switch back and forth between your IDE (editor)

* First, create a folder called `graphql-server-example` using the `mkdir` command.

      mkdir graphql-server-example

* Enter the directory, so the remaining work will take place within that directory.

      cd graphql-server-example

* Initialize the new directory as a Node.js project using the Node.js package manager, `npm`.

      npm init --yes

  >  We use `npm`, the default package manager which ships with Node.js.  Other package managers, such as [Yarn](//yarnpkg.com), offer similar functionality, but will not be covered in this guide.

If the above steps all completed successfully, there should be a new `package.json` file in the directory.  You can verify this by running `ls` (list files).

## Step 2: Install dependencies

Next, we'll install the two core dependencies which are necessary for responding to GraphQL requests:

* [`apollo-server`](//npm.im/apollo-server): The Apollo server library which allows you to focus on defining the shape of your data and how to fetch it.
* [`graphql`](//npm.im/graphql): The library used to build a schema and to execute queries on that schema.
  > Note: There won't be any usage of the `graphql` package in this guide, but it is required to be installed separately as it's an important "peer dependency" of Apollo Server.

While you could write all of the necessary code yourself, these two dependencies make it easier to build a GraphQL server and are common in applications of all sizes.

Run the following command to install both of these dependencies and save them in the project:

    npm install --save apollo-server graphql

In the next step, we'll use these dependencies to create a server which processes and responds to incoming GraphQL requests.

## Step 3: Create the server

In this step, we'll provide a code block which sets up `apollo-server` to respond to an incoming GraphQL request.  In order to move along quickly, we'll have you copy and paste the code into an `index.js` file in your project.  When looking at the code, we hope you'll find the comments helpful in understanding the core GraphQL concepts.  Don't worry if there is something which needs more explanation; we'll point you to the right places for more details at the end of this guide.

The example code will utilize a static collection of two books.  In a more complicated example, the books might be fetched from a web resource (e.g. Amazon or a local library's website) or a database (e.g. MySQL or MongoDB).

* Using the IDE/editor you've chosen (e.g. Visual Studio Code), open the `graphql-server-example` directory which we created in the first step.
  > In most editors, you can open a directory by selecting the "File" menu and then "Open".
* Create a new, blank file called `index.js` in the root of the project directory.
* "Copy" the following code block, "Paste" it into the `index.js` file you created in the previous step, then "Save" the file:

  ```js
  const { ApolloServer } = require('apollo-server');

  // This is a (sample) collection of books we'll be able to query
  // the GraphQL server for.  A more complete example might fetch
  // from an existing data source like a REST API or database.
  const books = [
    {
      title: 'Harry Potter and the Chamber of Secrets',
      author: 'J.K. Rowling',
    },
    {
      title: 'Jurassic Park',
      author: 'Michael Crichton',
    },
  ];

  // Type definitions define the "shape" of your data and specify
  // which ways the data can be fetched from the GraphQL server.
  const typeDefs = `
    # Comments in GraphQL are defined with the hash (#) symbol.

    # This "Book" type can be used in other type declarations.
    type Book {
      title: String
      author: String
    }

    # The "Query" type is the root of all GraphQL queries.
    # (A "Mutation" type will be covered later on.)
    type Query {
      books: [Book]
    }
  `;

  // Resolvers define the technique for fetching the types in the
  // schema.  We'll retrieve books from the "books" array above.
  const resolvers = {
    Query: {
      books: () => books,
    },
  };

  // In the most basic sense, the ApolloServer can be started
  // by passing type definitions (typeDefs) and the resolvers
  // responsible for fetching the data for those types.
  const server = new ApolloServer({ typeDefs, resolvers });

  // This `listen` method launches a web-server.  Existing apps
  // can utilize middleware options, which we'll discuss later.
  server.listen(({ url }) => {
    console.log(`Visit ${url}/graphiql to run queries!`);
  });
  ```

The code above includes everything that is necessary to get this basic GraphQL server running.  In the next step, we'll start the server so it's ready to respond to requests!

## Step 4: Start the server

For this step, we'll return to the terminal/console and start the server we defined in the previous steps.

* Run the `index.js` file we created in the previous step using Node.js

      node index.js

* You should see the following output from the above command:

      Visit http://localhost:3000/graphiql to run queries!
* Open the address provided in your web browser.
* If everything is working, you should see the GraphiQL explorer tool, which we will use in the next step.

> TODO: Image here.

In the next step, we'll use the GraphiQL tool to send queries to the GraphQL server.

## Step 5: Running your first query

At this point, you'll be able to start sending queries to the GraphQL server using the GraphiQL explorer, which is split into a few parts:

* The request (on the left)
* The response (on the right)
* The documentation (available using the "Docs" link in the top-right corner.

Since we're trying to obtain books...

> WIP / TODO ^

## Next steps

This application should be a great starting point for any GraphQL server, but the following resources are a great next step in building a GraphQL server:

* [Adding Apollo Server to an existing app]()
* [Schema design]()
* [Deployment]()

## More information

### GitHub Repository

The code from the above examples can be accessed in our [getting started example repository](.) on GitHub, which also includes instructions on how to get started in its [readme](.).
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTQxMDEwMDk1NiwtMjU0NDk1NjAwLC00MD
E0OTg0ODIsLTY1MTY5NDU5LC02OTM1MTk2NzQsLTE2ODY0NTMx
NzEsLTMwNjE4OTAzNCwxMDQ0ODgzMzQxLDM2NDc5MTY3NCwtNz
A0OTQ1ODQ4LC0xMjI3OTAzMjE5LDE1NDc5MTY3MjAsMTUwMDkx
NDM2OSwxODg3NDYyMjIyLC04ODc3MTkxNTksMTE2OTA0NDU1MS
wxNjE5MDI3NDQyLDE5OTc5NTU4NzEsMTgyMDI4NDk1OCwtMTk1
Mjc0NDExXX0=
-->