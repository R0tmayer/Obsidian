Всего существует 3 подхода чтобы связать Principal (parent) и Dependent (child):
1. ParentId + ParentEntity
2. ParentId + OnModelCreating
3. ParentEntity + OnModelCreating (создаётся Shadow foreign key)

#### ParentId + ParentEntity
Самый простой способ. Foreign key у зависимой сущности присваивается автоматически

```csharp
// Principal (parent)
public class Blog
{
    public int Id { get; set; }
    public ICollection<Post> Posts { get; } = new List<Post>(); // Collection navigation containing dependents
}

// Dependent (child)
public class Post
{
    public int Id { get; set; }
    public int BlogId { get; set; } // Required foreign key property
    public Blog Blog { get; set; } = null!; // Required reference navigation to principal
}
```

Нужно отметить, что если `BlogId` будет nullable, то и `Blog` тоже должен быть nullable
```csharp
public class Post
{
    public int Id { get; set; }
    public int? BlogId { get; set; } // Required foreign key property
    public Blog? Blog { get; set; } = null!; // Required reference navigation to principal
}
```

#### ParentId + OnModelCreating
Если в зависимой сущности не хочется указывать B