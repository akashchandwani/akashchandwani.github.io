---
title: "Efficient Data Modeling: Hibernate Strategies for Shared Columns"
date: 2021-04-21T14:28:39+05:30
draft: false
tags: ["java", "hibernate", "orm"]
---

## Introduction

In database tables, common columns are often used to store metadata about entries, serving purposes such as auditing, multi-tenancy, and soft deletion. These common columns may include information like `created_by`, `updated_by`, `created_at`, and `last_modified_at`. While it's possible to duplicate these columns in entity objects, there's a more efficient way to handle this. Let's explore that.

## Scenario

Consider a scenario where a set of resource tables shares common columns, such as `created_at` and `last_modified_at`. When mapping these tables to (javax.persistence) entities, we notice that all entity classes have common fields like `created_at` and `last_modified_at`.

## Implementation

To adhere to the DRY (Don't Repeat Yourself) principle and leverage inheritance, we can create a parent class named `ParentEntity.java` to encapsulate these common attributes. Since we don't intend to create an object of this class, let's make it abstract.

We'll also use Hibernate's `@MappedSuperclass` annotation on the parent class to map these attributes in classes that inherit from it. The `ParentEntity` class looks like this:

```java {linenos=table,hl_lines=["4-5"],linenostart=1}
import javax.persistence.MappedSuperclass;
import java.time.Instant;

@MappedSuperclass
public abstract class ParentEntity {

    private Instant createdAt;
    private Instant lastModifiedAt;

    public Instant getLastModifiedAt() {
        return lastModifiedAt;
    }

    public void setCreatedAt(Instant createdAt) {
        this.createdAt = createdAt;
    }

    public void setLastModifiedAt(Instant lastModifiedAt) {
        this.lastModifiedAt = lastModifiedAt;
    }

    public Instant getCreatedAt() {
        return createdAt;
    }
}
```

Now, for any entity that requires these columns in the database, simply extend this base class. The @MappedSuperclass annotation automatically maps these common columns to the entity when inherited.

Here's a sample class, Item.java, that inherits the properties from the base class while preserving the database mapping of the common columns:

```java {linenos=table,hl_lines=[5],linenostart=1}
import javax.persistence.Entity;
import javax.persistence.Id;

@Entity
public class Item extends ParentEntity {

    @Id
    private Integer id;

    private String name;

    public Integer getId() {
        return id;
    }

    public void setId(Integer id) {
        this.id = id;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }
}
```

I trust this blog provides valuable insights.
