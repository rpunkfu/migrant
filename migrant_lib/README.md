# migrant_lib

> Embeddable migration management

`migrant_lib` allows defining and embedding management of migration in your shipped app.


```rust
config.use_migrations(vec![
    FileMigration::with_tag("initial")?
        .up("migrations/initial/up.sql")?
        .down("migrations/initial/down.sql")?
        .boxed(),
    FileMigration::with_tag("second")?
        .up("migrations/second/up.sql")?
        .down("migrations/second/down.sql")?
        .boxed(),
    FnMigration::with_tag("custom")?
        .up(migrations::Custom::up)
        .down(migrations::Custom::down)
        .boxed(),
])?;
```


Migrations can be defined as files or functions. Migration files must exist at runtime.
Migration tags must all be unique. Function migrations must have the signature
`fn(DbConn) -> Result<(), Box<std::error::Error>>`. See the
[programmable example](https://github.com/jaemk/migrant/blob/master/migrant_lib/examples/programmable.rs)
for a working sample.

Migrations management identical to [`migrant`](https://github.com/jaemk/migrant) cli tool can also be embedded.
This method only supports file-base migrations generated by `migrant_lib` (or `migrant` cli). See the
[embedded example](https://github.com/jaemk/migrant/blob/master/migrant_lib/examples/embed.rs)
for a working sample.
