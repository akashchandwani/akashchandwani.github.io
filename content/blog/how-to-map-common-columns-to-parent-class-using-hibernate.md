---
title: "How to Map Common Columns to Parent Class Using Hibernate"
date: 2021-04-21T14:28:39+05:30
draft: false
tags: ["java", "hibernate", "orm"]
---

## Introduction

We tend to have some common columns in our database tables to store the metadata about the entries in our database tables. The reasons can be one the following —

1. Auditing — To track who and when a person user updated a row in a table. This is usually done using a common set of columns in each table like — created_by, updated_by, created_at, last_modified_at.
2.  Multi-tenancy — To store the Id of tenant which owns the resource. One of the implementation of multi tenancy is storing all the entities in a single database and separating them by a special column stored in every table.
3.  Soft Delete — To logically delete a row in the table without removing it from the database. For this, one can choose to maintain a `is_deleted` column in each of the tables to know whether an entity has been logically deleted or not.

Thus, we understand that there could be multiple scenarios (which are not limited to the ones discussed above) where there could be a need to have a common set of columns to store the metadata of the tables. But does it mean we’ll have to duplicate those column entries in our Entity Objects? Well of course you can do it, but there is a smart way to do it. Let’s discuss about that a bit more.

## Scenario

Let’s assume we have a set of resource tables, which contains the common columns — `created_at` and `last_modified_at`. Once we start mapping these database tables to (javax.persistent) entities, we’ll observer that all those entity classes would have a common fields called created_at and last_modified_at.

## Let’s do it

Well, we know inheritance and we know that we should not repeat ourselves (DRY Principle). Let’s use basic inheritance and pull those attributes out and put it into a parent class, let’s call that class `ParentEntity.java`. Also, since we don’t intend to create an object of this class, let’s make this class an abstract class.

Also, let’s perform our hibernate magic here. Let’s use the annotation @MappedSuperClass on the parent class to map these attributes in the class which inherits from this class. Our `ParentEntity` class would look like this —

```java
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

Now, for any entity that should have these columns in the database, just extend this base class, and that’s all you had to do. The annotation `@MappedSuperClass` would map these common columns to the entity when inherited from this class.

Below is a sample class — `Item.java` that inherits the properties from the base class and preserves the database mapping of the common columns.

```java
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

I hope the blog was informative.
