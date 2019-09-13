# Test for Identity on CosmosDB from Blazor Server (preview9)

Referenced at https://github.com/aspnet/EntityFrameworkCore/issues/17829

Using Cosmos DB as the database for identity in a preview9 Blazor Server app crashes when a user attempts to register an account,
showing the screen below. This repo is has with change to the out-of-the-box Blazor 
Server template app. To recreate, download the project, use the Azure Cosmos DB Emulator and update the connection parameters 
accordingly in the call to services.AddDbContext in Startup.cs (code snippet below).

# Code snippet from Startup.cs

```
            // =============================================================================
            // Updated to target local Cosmos DB rathern than local SQL Server
            // Note: you will need to change the Key "C2y..." for your Cosmos connection
            // =============================================================================
            //services.AddDbContext<ApplicationDbContext>(options =>
            //    options.UseSqlServer(
            //        Configuration.GetConnectionString("DefaultConnection")));
            services.AddDbContext<ApplicationDbContext>(options =>
                options.UseCosmos(
                    "https://localhost:8081",
                    "C2y6yDjf5/R+ob0N8A7Cgv30VRDJIWEHLM+4QDU5DE2nQ9nDuVTqobD4b8mGGyPMbIZnqyMsEcaGQy67XIw/Jw==",
                    "BlazorIdentity"));
            // =============================================================================
            // End of changes
            // =============================================================================
```

# Screen grab immediately after attempting to register a new user
![image](https://user-images.githubusercontent.com/11708435/64855895-c25dd800-d618-11e9-9a7f-27ef3fd67c28.png)
