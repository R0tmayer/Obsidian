Всего существует 3 подхода чтобы связать Principal (parent) и Dependent (child):
1. Required one-to-many
2. One-to-many without navigation to principal
3. Required one-to-many with shadow foreign key

####  Required one-to-many
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

##### Optional one-to-many
Нужно отметить, что если `BlogId` будет nullable, то и `Blog` тоже должен быть nullable
```csharp
public class Post
{
    public int Id { get; set; }
    public int? BlogId { get; set; } // Required foreign key property
    public Blog? Blog { get; set; } = null!; // Required reference navigation to principal
}
```

#### One-to-many without navigation to principal
Если в зависимой сущности не хочется указывать навигационное поле `Blog Blog`, то придётся делать так:
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
}
```

И создать конфигурацию для `Blog`:
```csharp
protected override void OnModelCreating(ModelBuilder modelBuilder)
{
    modelBuilder.Entity<Blog>()
        .HasMany(e => e.Posts)
        .WithOne()
        .HasForeignKey(e => e.BlogId)
        .IsRequired();
}
```
Или конфигурацию для `Post`:
```csharp
protected override void OnModelCreating(ModelBuilder modelBuilder)
{
    modelBuilder.Entity<Post>()
        .HasOne<Blog>()
        .WithMany(e => e.Posts)
        .HasForeignKey(e => e.BlogId)
        .IsRequired();
}
```

#### Required one-to-many with shadow foreign key
Если хочется указать только навигационное поле `Blog Blog`:
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
}
```