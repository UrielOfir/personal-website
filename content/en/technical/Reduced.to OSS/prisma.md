---
title: "Prisma"
weight: 1
type: "docs"
description: >
  Simplifying Database Work for Developers
---

Prisma is an open-source database toolkit that makes it easier for developers to interact with their databases. It serves as an intermediary layer between the database and the application code, offering several tools and features that simplify database operations. In this article, I will provide a breakdown of what Prisma does, and to give you a clearer understanding, I'll illustrate its use with practical examples from the "Reduced.to" project. These examples will demonstrate how Prisma can be effectively utilized in a real-world application, showcasing its functionality and ease of use in a TypeScript-based project.

1. ### ORM (Object-Relational Mapping)  
   **Simplifies Data Access:** Prisma is often described as an ORM (Object-Relational Mapping) tool. It allows developers to write database queries using simple and straightforward JavaScript or TypeScript code, rather than complex SQL queries.  
   **Code-First Approach:** With Prisma, you define your database schema in a human-readable format directly in your code, and Prisma generates the necessary SQL for you. This approach is known as a "code-first" approach and is particularly appealing for developers who prefer to work within their codebase without switching contexts.
2. ### Prisma Schema  
   **Central Configuration:** The Prisma schema file is the heart of your Prisma setup. It's where you define your database models, relationships, and generate client code.  
   **Type-Safe:** The Prisma schema helps in generating a type-safe database client, ensuring that your database queries are checked for type correctness at compile time. This feature significantly reduces runtime errors and bugs related to database operations.
3. ### Prisma Client  
   **Auto-Generated and Type-Safe:** Prisma Client is an auto-generated database client that lets you read and write data in your database in a type-safe manner. It translates the operations written in JavaScript or TypeScript into actual SQL queries.  
   **Developer-Friendly:** The Prisma Client API is designed to be intuitive and straightforward, making data access and manipulation a lot easier and more efficient. It provides a fluent API for constructing and running database queries.
4. ### Prisma Migrate
   **Easy Database Migrations:** Prisma Migrate is a powerful tool for managing changes to your database schema. It helps in evolving the database schema over time, using migration files that can be version-controlled. It makes setting up and updating the database structure much simpler.
5. ### Prisma Studio
   **Visual Data Management:** Prisma Studio is a GUI (Graphical User Interface) to view and edit data in your database. It's an easy way for developers and team members to inspect and manipulate database records without writing SQL queries.

# Practical Use of Prisma in Reduced.to
To give you a real-world example of how Prisma is used, let's look at some code snippets from the "Reduced.to" project.

### Prisma Schema Example: Defining the Links Table
In the Reduced.to project, the Prisma schema is used to define the structure of the database.   
Here's how the Link model is defined in the project's **schema.prisma** file:

``` prisma
model Link {
  id             String    @id @default(uuid())
  key            String    @unique // Unique key of the link
  url            String
  favicon        String?
  password       String?
  user           User?     @relation(fields: [userId], references: [id], onDelete: Cascade)
  userId         String
  description    String?
  expirationTime DateTime?
  createdAt      DateTime  @default(now())
  Report         Report[]
  clicks         Int       @default(0)
  visit          Visit[]

  @@index(userId)
  @@index(key)
  @@index([url, clicks])
}
```
#### Explanation:
**Model Declaration:** model Link declares a new model corresponding to a table in the database.
**Fields:** Each line under the model declaration represents a column in the Link table with its data type and constraints (e.g., @id, @default, @unique).
**Relations:** The user field establishes a relation to the User model. The onDelete: Cascade part indicates that if the related user is deleted, associated links will also be deleted.
**Indexes:** The @@index annotations are used to optimize queries based on these fields.

### Using Prisma Client: Deleting a Link
In the links.service.ts file of the backend application, Prisma Client is used to interact with the database.   
Here's an example of how a link is deleted:

``` typescript
delete(id: string): Promise<Link> {
  return this.prismaService.link.delete({
    where: {
        id,
    },
    include: {
        visit: true,
    },
  });
}
```

#### Explanation:
**Function Definition:** The delete function takes an id parameter and returns a Promise that resolves to a Link object.  
**Prisma Delete Operation:** this.prismaService.link.delete is a Prisma Client method that deletes a record from the Link table.  
**Where Clause:** The where option specifies the criteria for selecting the record to delete, which in this case, is based on the provided id.  
**Include Option**: The include option with "visit: true" specifies that the related Visit records should also be fetched and included in the response when a link is deleted.   
<br>


These examples from "Reduced.to" show Prisma's capabilities in defining data models and performing database operations in a concise, readable, and maintainable way. This makes Prisma an invaluable tool in modern web development, especially in TypeScript-based projects.