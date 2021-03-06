---
slug: mix-tool
title: Mix features into ASP.NET Core Projects from Gists
---

To complete the picture of making it easy as possible to compose ASP.NET Core Apps we've created the `mix` dotnet tool to easily 
install features which can be installed with:

    $ dotnet tool install --global mix

The same functionality is also built into the cross-platform [web](/web-tool) and Windows [`app`](/netcore-windows-desktop) 
dotnet tools which can be updated to the latest version with:

    $ dotnet tool update -g web
    $ dotnet tool update -g app

### mix-enabled dotnet tools

`mix` works exactly the same in all dotnet tools, which just needs the **tool name prefixed** before the `mix` command:

    $ mix ...
    $ web mix ...
    $ app mix ...

### mix Usage

The `mix` tool is designed around applying ASP.NET Core features captured in GitHub gists to your local .NET Core projects. 

Type `mix ?` for a quick Usage Summary:

```
View all published gists:
   mix

Simple Usage:
   mix <name> <name> ...

Mix using numbered list index instead:
   mix 1 3 5 ...

Delete previously mixed gists:
   mix -delete <name> <name> ...

Use custom project name instead of current folder name (replaces MyApp):
   mix -name ProjectName <name> <name> ...

Replace additional tokens before mixing:
   mix -replace term=with <name> <name> ...

Multi replace with escaped string example:
   mix -replace term=with -replace "This Phrase"="With This" <name> <name> ...

Only display available gists with a specific tag:
  mix #<tag>
  mix #<tag>,<tag>,<tag>
```

Although most of the time you're only going to run 2 commands, viewing available features with:

    $ mix

Where it displays different features that can be added to your App, where they're added to and the author of the Gist:

```
 1. init                 Empty .NET Core 2.2 ServiceStack App         to: .      by @ServiceStack  [project]
 2. init-lts             Empty .NET Core 2.1 LTS ServiceStack App     to: .      by @ServiceStack  [project]
 3. init-corefx          Empty ASP.NET Core 2.1 LTS on .NET Framework to: .      by @ServiceStack  [project]
 4. init-sharp-app       Empty ServiceStack Sharp App                 to: .      by @ServiceStack  [project]
 5. bootstrap-sharp      Bootstrap + #Script Pages Starter Template   to: $HOST  by @ServiceStack  [ui,sharp]
 6. redis                Use ServiceStack.Redis                       to: $HOST  by @ServiceStack  [db]
 7. sqlserver            Use OrmLite with SQL Server                  to: $HOST  by @ServiceStack  [db]
 8. sqlite               Use OrmLite with SQLite                      to: $HOST  by @ServiceStack  [db]
 9. postgres             Use OrmLite with PostgreSQL                  to: $HOST  by @ServiceStack  [db]
10. mysql                Use OrmLite with MySql                       to: $HOST  by @ServiceStack  [db]
11. oracle               Use OrmLite with Oracle                      to: $HOST  by @ServiceStack  [db]
12. firebird             Use OrmLite with Firebird                    to: $HOST  by @ServiceStack  [db]
13. dynamodb             Use AWS DynamoDB and PocoDynamo              to: $HOST  by @ServiceStack  [db]
14. mongodb              Use MongoDB                                  to: $HOST  by @ServiceStack  [db]
15. ravendb              Use RavenDB                                  to: $HOST  by @ServiceStack  [db]
16. marten               Use Marten NoSQL with PostgreSQL             to: $HOST  by @ServiceStack  [db]
17. auth                 Configure AuthFeature                        to: $HOST  by @ServiceStack  [auth]
18. auth-db              Use OrmLite Auth Repository (requires auth)  to: $HOST  by @ServiceStack  [auth]
19. auth-redis           Use Redis Auth Repository (requires auth)    to: $HOST  by @ServiceStack  [auth]
20. auth-memory          Use Memory Auth Repository (requires auth)   to: $HOST  by @ServiceStack  [auth]
21. auth-dynamodb        Use DynamoDB Auth Repository (requires auth) to: $HOST  by @ServiceStack  [auth]
22. auth-mongodb         Use MongoDB Auth Repository (requires auth)  to: $HOST  by @ServiceStack  [auth]
23. auth-ravendb         Use RavenDB Auth Repository (requires auth)  to: $HOST  by @ServiceStack  [auth]
24. auth-marten          Use Marten Auth Repository (requires auth)   to: $HOST  by @ServiceStack  [auth]
25. backgroundmq         Use Memory Background MQ                     to: $HOST  by @ServiceStack  [mq]
26. rabbitmq             Use RabbitMQ                                 to: $HOST  by @ServiceStack  [mq]
27. sqs                  Use AWS SQS MQ                               to: $HOST  by @ServiceStack  [mq]
28. servicebus           Use Azure Service Bus MQ                     to: $HOST  by @ServiceStack  [mq]
29. redismq              Use Redis MQ                                 to: $HOST  by @ServiceStack  [mq]
30. vue-lite-lib         Update vue-lite projects libraries           to: $HOST  by @ServiceStack  [lib,vue]
31. react-lite-lib       Update react-lite projects libraries         to: $HOST  by @ServiceStack  [lib,react]
32. validation-contacts  Contacts Validation Example                  to: $HOST  by @ServiceStack  [example]
33. feature-mq           Simple MQ Feature to test sending Messages   to: $HOST  by @ServiceStack  [feature,mq]
34. feature-authrepo     List and Search Users registered in AuthRepo to: $HOST  by @ServiceStack  [feature]
37. docker               Dockerfile example for .NET Core Sharp Apps  to: .      by @ServiceStack  [config]
38. svg-action           Material Design Action Icons                 to: svg/   by @ServiceStack  [svg]
39. svg-alert            Material Design Alert Icons                  to: svg/   by @ServiceStack  [svg]
40. svg-av               Material Design Audio Visual Icons           to: svg/   by @ServiceStack  [svg]
41. svg-communication    Material Design Communication Icons          to: svg/   by @ServiceStack  [svg]
42. svg-content          Material Design Content Icons                to: svg/   by @ServiceStack  [svg]
43. svg-device           Material Design Device Icons                 to: svg/   by @ServiceStack  [svg]
44. svg-editor           Material Design Editor Icons                 to: svg/   by @ServiceStack  [svg]
45. svg-file             Material Design File Icons                   to: svg/   by @ServiceStack  [svg]
46. svg-hardware         Material Design Hardware Icons               to: svg/   by @ServiceStack  [svg]
47. svg-image            Material Design Image Icons                  to: svg/   by @ServiceStack  [svg]
48. svg-maps             Material Design Maps Icons                   to: svg/   by @ServiceStack  [svg]
49. svg-navigation       Material Design Navigation Icons             to: svg/   by @ServiceStack  [svg]
50. svg-places           Material Design Places Icons                 to: svg/   by @ServiceStack  [svg]
51. svg-social           Material Design Social Icons                 to: svg/   by @ServiceStack  [svg]
52. svg-toggle           Material Design Toggle Icons                 to: svg/   by @ServiceStack  [svg]


   Usage:  mix <name> <name> ...

  Search:  mix #<tag> Available tags: auth, config, db, feature, lib, mq, project, react, sharp, svg, ui, vue

Advanced:  mix ?
```

Then choosing which features you want to add to your project with `mix <name>`, e.g:

    $ mix redis

The entire list of available features is maintained in the self-documenting human and machine readable
[mix.md](https://gist.github.com/gistlyn/9b32b03f207a191099137429051ebde8) feature index.

> To publish your feature here and make it available to all `mix` users, please [link to it in the comments](https://gist.github.com/gistlyn/9b32b03f207a191099137429051ebde8#comments).

### Mix in Features into ASP.NET Core Apps

It should be noted that `ModularStartup` and `mix` dotnet tool aren't limited to ServiceStack Apps, they're a generic solution
that can easily add features to any .NET Core App. E.g. some of ServiceStack features relies on external dependencies which utilizes
the same dependency registration used in all ASP.NET Core Apps, e.g running:

    $ mix mongodb

Applies the `mongodb` feature to your HOST project as instructed by the `to: $HOST` modifier above that it finds by
using the first folder containing either `appsettings.json`, `Program.cs` or `Startup.cs`
and writing the following [mongodb Gist file](https://gist.github.com/gistlyn/f777396583262127a66e2369ae475d3f):

```csharp
namespace MyApp
{
    public class ConfigureMongoDb : IConfigureServices
    {
        IConfiguration Configuration { get; }
        public ConfigureMongoDb(IConfiguration configuration) => Configuration = configuration;

        public void Configure(IServiceCollection services)
        {
            var mongoClient = new MongoClient();
            IMongoDatabase mongoDatabase = mongoClient.GetDatabase("MyApp");
            container.AddSingleton(mongoDatabase);
        }
    }    
}
```

With all `MyApp` tokens replaced with the **Project Name** using the same replacement rules as new projects, i.e:

 - `MyApp` will be replaced with `ProjectName`
 - `my-app` will be replaced with `project-name`
 - `My App` will be replaced with `Project Name`

By default it assumes the folder name is the project name, that's overridable using the `-name` flag:

    $ mix -name ProjectName mongodb

This feature also installs the **MongoDB.Driver** NuGet package as instructed by the `_init` command in the 
[mongodb feature](https://gist.github.com/gistlyn/f777396583262127a66e2369ae475d3f).

So after just a single `mix` command and App restart, it's now configured and running with MongoDB!

#### Registering MongoDB Auth Repository

As a design goal `mix` features are designed to be layerable where you can existing features that builds upon existing registrations, 
for example you can later configure your App to **enable auth** and configure it to use a `MongoDbAuthRepository` with:

    $ mix auth auth-mongodb

### Mix in DB Support

All DB servers are just as easily configurable, which we can quickly find using a `[db]` tag search:

    $ mix #db

Which will list all available `[db]` providers:

```
Results matching tag [db]:

   1. redis      Use ServiceStack.Redis            to: $HOST  by @ServiceStack  [db]
   2. sqlserver  Use OrmLite with SQL Server       to: $HOST  by @ServiceStack  [db]
   3. sqlite     Use OrmLite with SQLite           to: $HOST  by @ServiceStack  [db]
   4. postgres   Use OrmLite with PostgreSQL       to: $HOST  by @ServiceStack  [db]
   5. mysql      Use OrmLite with MySql            to: $HOST  by @ServiceStack  [db]
   6. oracle     Use OrmLite with Oracle           to: $HOST  by @ServiceStack  [db]
   7. firebird   Use OrmLite with Firebird         to: $HOST  by @ServiceStack  [db]
   8. dynamodb   Use AWS DynamoDB and PocoDynamo   to: $HOST  by @ServiceStack  [db]
   9. mongodb    Use MongoDB                       to: $HOST  by @ServiceStack  [db]
  10. ravendb    Use RavenDB                       to: $HOST  by @ServiceStack  [db]
  11. marten     Use Marten NoSQL with PostgreSQL  to: $HOST  by @ServiceStack  [db]

   Usage:  mix <name> <name> ...

  Search:  mix #<tag> Available tags: auth, config, db, feature, lib, mq, project, react, sharp, svg, ui, vue

Advanced:  mix ?
```

So we can install Redis with:

    $ mix redis

Where it will apply the [Redis Gist](https://gist.github.com/gistlyn/512309b3cb7d734bb0f7323907499b08) below:

```csharp
namespace MyApp
{
    public class ConfigureRedis : IConfigureServices, IConfigureAppHost
    {
        IConfiguration Configuration { get; }
        public ConfigureRedis(IConfiguration configuration) => Configuration = configuration;

        public void Configure(IServiceCollection services)
        {
            services.AddSingleton<IRedisClientsManager>(
                new RedisManagerPool(Configuration.GetConnectionString("Redis") ?? "localhost:6379"));
        }

        public void Configure(IAppHost appHost)
        {
            appHost.GetPlugin<SharpPagesFeature>()?.ScriptMethods.Add(new RedisScripts());
        }
    }
}
```

The configuration is declarative where it only runs `Configure(IAppHost appHost)` in ServiceStack Apps and only adds the `RedisScripts`
if it's configured with [#Script Pages](https://sharpscript.net/docs/sharp-pages), otherwise any additional configuration is inert and isn't run.

Typically DB's will require you to specify your App DB's connection string to your external DB (with a default fallback) - where typically the
most effort required to enable a feature is adding a Connection String in your `appsettings.json`.

### Composable Features

A nice characteristic about "no-touch" layerable features are that they're composable, where `mix` will let you hand-pick all features you
want in a single command. For example you can enable Authentication, register an RDBMS Auth Repository using SQL Server with:

    $ mix auth auth-db sqlserver

Which will apply the [Configure.Auth.cs](https://gist.github.com/gistlyn/1ec54e10d44f87e0f20daaf7e2248fea), 
[Configure.AuthRepository.cs](https://gist.github.com/gistlyn/16fddde0763b3eee516d670ab9fab194) and [Configure.Db.cs](https://gist.github.com/gistlyn/7075e53e1fe69d3da12996677b5f3a5a) gists.

If you later wanted to switch to PostgreSQL, you can `mix` it in with:

    $ mix postgres

Where it will override [Configure.Db.cs](https://gist.github.com/gistlyn/faf62da8b8ef30849506631025a5d06c) to use the postgres version, 
leaving any custom logic in `Configure.Auth.cs` or `Configure.AuthRepository.cs` untouched.

Or if you later want to change the Auth Repository to use Redis instead, you can run:

    $ mix auth-redis

Where it will override the existing `Configure.AuthRepository.cs` added by **auth-db**.

### Undo mix

In addition to being easy to add, `mix` makes it easy to undo where you can specify the `-delete` flag to remove all the Gist files added
by all features, e.g:

    $ mix -delete auth auth-db sqlserver

Which will let you review all the files in each Gist that will deleted, then hit `Enter` to confirm:

```
Delete 1 file from 'auth' https://gist.github.com/gistlyn/1ec54e10d44f87e0f20daaf7e2248fea:

C:\Projects\app\Configure.Auth.cs

Delete 1 file from 'auth-db' https://gist.github.com/gistlyn/16fddde0763b3eee516d670ab9fab194:

C:\Projects\app\Configure.AuthRepository.cs

Delete 1 file from 'sqlserver' https://gist.github.com/gistlyn/7075e53e1fe69d3da12996677b5f3a5a:

C:\Projects\app\Configure.Db.cs

Proceed? (n/Y):
```

### Encapsulated Features

A nice benefit of decoupling features into modular classes is that you're able to a richer and more customizable out-of-the-box experience. 

Instead of overloading users with daunting amounts of configuration required in common medium-sized Apps,
most templates will start with an empty slate and leave it for users to read about each feature then decide how to hand-pick 
different configuration to slot it into their own App's configuration. 

On the flip-side if you provide too much configuration Developers wont be confident to know what configuration belongs to which feature
and which feature are interconnected or can be safely removed without breaking their App.

With modular features we can encapsulate configuration in a single `.cs` file that's primed with the popular well-known configuration
for the feature. E.g. The Auth Repositories include an example of maintaining a custom `UserAuth` model, registering the 
[Auth Event](/sessions#session-events) to populate their additional fields on Authentication and sample code necessary for ensuring
a specific Admin User is created on `Startup`:

```csharp
namespace MyApp
{
    // Custom User Table with extended Metadata properties
    public class AppUser : UserAuth
    {
        public string ProfileUrl { get; set; }
        public string LastLoginIp { get; set; }
        public DateTime? LastLoginDate { get; set; }
    }

    public class AppUserAuthEvents : AuthEvents
    {
        public override void OnAuthenticated(IRequest req, IAuthSession session, IServiceBase authService, 
            IAuthTokens tokens, Dictionary<string, string> authInfo)
        {
            var authRepo = HostContext.AppHost.GetAuthRepository(req);
            using (authRepo as IDisposable)
            {
                var userAuth = (AppUser)authRepo.GetUserAuth(session.UserAuthId);
                userAuth.ProfileUrl = session.GetProfileUrl();
                userAuth.LastLoginIp = req.UserHostAddress;
                userAuth.LastLoginDate = DateTime.UtcNow;
                authRepo.SaveUserAuth(userAuth);
            }
        }
    }

    public class ConfigureAuthRepository : IConfigureAppHost, IConfigureServices, IPreInitPlugin
    {
        public void Configure(IServiceCollection services)
        {
            services.AddSingleton<IAuthRepository>(c =>
                new OrmLiteAuthRepository<AppUser, UserAuthDetails>(c.Resolve<IDbConnectionFactory>()) {
                    UseDistinctRoleTables = true
                });            
        }

        public void Configure(IAppHost appHost)
        {
            var authRepo = appHost.Resolve<IAuthRepository>();
            authRepo.InitSchema();

            CreateUser(authRepo, "admin@email.com", "Admin User", "p@55wOrd", roles:new[]{ RoleNames.Admin });
        }

        public void BeforePluginsLoaded(IAppHost appHost)
        {
            appHost.AssertPlugin<AuthFeature>().AuthEvents.Add(new AppUserAuthEvents());
        }

        // Add initial Users to the configured Auth Repository
        public void CreateUser(IAuthRepository authRepo, 
            string email, string name, string password, string[] roles)
        {
            if (authRepo.GetUserAuthByUserName(email) == null)
            {
                var newAdmin = new AppUser { Email = email, DisplayName = name };
                var user = authRepo.CreateUserAuth(newAdmin, password);
                authRepo.AssignRoles(user, roles);
            }
        }
    }
}
```

All captured within a working configuration. You can start appreciating the instant utility of `mix` once you imagine what it was like before 
with how much time an effort it would've taken to scan through docs, learn about each feature independently to be able to piece together 
equivalent functionality.

### Mix in Auth Repository

As it can take a while to piece together how to configure your preferred Auth Repository, use a Custom User Model 
and utilize [Auth Events](/sessions#session-events) to populate it, we now recommend using `mix` to configure
your preferred Auth Repository, which you can query with:

    $ mix #auth

To display the current list of available Auth Repositories:

```
Results matching tag [auth]:

   1. auth              Configure AuthFeature                        to: $HOST  by @ServiceStack [auth]
   2. auth-db           Use OrmLite Auth Repository (requires auth)  to: $HOST  by @ServiceStack [auth]
   3. auth-redis        Use Redis Auth Repository (requires auth)    to: $HOST  by @ServiceStack [auth]
   4. auth-memory       Use Memory Auth Repository (requires auth)   to: $HOST  by @ServiceStack [auth]
   5. auth-dynamodb     Use DynamoDB Auth Repository (requires auth) to: $HOST  by @ServiceStack [auth]
   6. auth-mongodb      Use MongoDB Auth Repository (requires auth)  to: $HOST  by @ServiceStack [auth]
   7. auth-ravendb      Use RavenDB Auth Repository (requires auth)  to: $HOST  by @ServiceStack [auth]
   8. auth-marten       Use Marten Auth Repository (requires auth)   to: $HOST  by @ServiceStack [auth]
   9. feature-authrepo  List and Search Users in an Auth Repo        to: $HOST  by @ServiceStack [feature,auth]
```

### Mix in MQ Server

Likewise we now recommend using `mix` to configure your preferred MQ Service, other than being quicker to add,
it proposes adopting a naming convention in app settings and file names that other `mix` features can also make use of:

    $ mix #mq

Currently available list of MQ Services:

```
Results matching tag [mq]:

   1. backgroundmq  Use Memory Background MQ                    to: $HOST  by @ServiceStack  [mq]
   2. rabbitmq      Use RabbitMQ                                to: $HOST  by @ServiceStack  [mq]
   3. sqs           Use AWS SQS MQ                              to: $HOST  by @ServiceStack  [mq]
   4. servicebus    Use Azure Service Bus MQ                    to: $HOST  by @ServiceStack  [mq]
   5. redismq       Use Redis MQ                                to: $HOST  by @ServiceStack  [mq]
   6. feature-mq    Simple MQ Feature to test sending Messages  to: $HOST  by @ServiceStack  [feature,mq,sharp]
```

## Mix in NUglify

You can configure your ServiceStack App to use Nuglify's Advanced HTML, CSS, JS Minifiers using [mix](/mix-tool) with:

    $ mix nuglify 

Which will write [Configure.Nuglify.cs](https://gist.github.com/gistlyn/4bdb79d21f199c22b8a86f032c186e2d) to your **HOST** project.

### Mix in Prebuilt Recipes and Working Examples

`ModularStartup` and `mix` can scale up to complete working examples which can provide instant utility and integration of a feature into
your existing App. By contrast most working examples are typically made available off to the side in stale projects which need to 
be downloaded and run in isolation. If it still works you'd then have to compare the project files with your project and carefully copy over the 
differences you'd think your App needs to replicate its functionality. This can be very time consuming to the point where a lot of users will 
skip trying to download & run the example and instead try to manually configure it in their App.

All `mix` features add their files to your App's [Physical Project Structure](/physical-project-structure) where configuration is added to 
your `Host` Project, Service Contracts are added to your `ServiceModel/` folder and Service Implementations added to your `ServiceInterface/` folder
and any Web assets added to your App's `wwwroot/`. 

They can also be added to both multi and single project solutions in which case they'll be added to `ServiceInterface` and `ServiceModel` folders 
in your App's project folder using the same namespace as used in multi-project solutions, making it easy to upgrade to a multi-project solution later.

### example-validation

The `example-validation` **mix** is a complete working validation example that's typical of a real-world validation example complete with 
Authentication integration allowing each authenticated user to manage their own private Contacts list. 

[![](https://raw.githubusercontent.com/ServiceStack/docs/master/docs/images/mix/example-validation-900.gif)](https://youtu.be/udrLtICylj8)

> YouTube: [youtu.be/udrLtICylj8](https://youtu.be/udrLtICylj8)

To follow video's example, start with a new **Acme** project from `sharp` .NET Core Template:

    $ web new script Acme

Add the `example-validation` mix:

    $ cd Acme
    $ web mix example-validation

Which will prompt you with a link to the gist and the files that will be added to your project:

```
Write files from 'example-validation' https://gist.github.com/gistlyn/33873ed2857b2c5a9623629c6210d665 to:

  C:\projects\Acme\Acme\Configure.Contacts.cs
  C:\projects\Acme\Acme.ServiceInterface\ContactServices.cs
  C:\projects\Acme\Acme.ServiceModel\Contacts.cs
  C:\projects\Acme\Acme\wwwroot\contacts\_id\edit.html
  C:\projects\Acme\Acme\wwwroot\contacts\_requires-auth-partial.html
  C:\projects\Acme\Acme\wwwroot\contacts\index.html

Proceed? (n/Y):
```

Now after restarting your App you'll be able to add contacts by clicking on the new **Contacts** link in your App's main menu: 

    $ cd Acme
    $ dotnet run

After you're done reviewing the example you can either refactor it to handle your App's requirements or completely remove it from your App with:

    $ mix -delete example-validation

### feature-mq

The `feature-mq` adds MQ support to your App, complete with UI and includes 2 different ways of calling MQ Services in ServiceStack, just like 
`example-validation` above, `feature-mq` is another complete working example with both UI and Service implementation in the following files:

  - [Configure.Mq.cs?](https://gist.github.com/gistlyn/355338cd60a32ee9c9fc4761269f7782#file-configure-mq-cs)
  - [Feature.Mq.cs](https://gist.github.com/gistlyn/355338cd60a32ee9c9fc4761269f7782#file-feature-mq-cs)
  - [ServiceInterface\MqServices.cs ](https://gist.github.com/gistlyn/355338cd60a32ee9c9fc4761269f7782#file-serviceinterface-mqservices-cs)
  - [ServiceModel\Mq.cs](https://gist.github.com/gistlyn/355338cd60a32ee9c9fc4761269f7782#file-servicemodel-mq-cs)
  - [wwwroot\messaging.html](https://gist.github.com/gistlyn/355338cd60a32ee9c9fc4761269f7782#file-wwwroot-messaging-html)
  
As `Configure.Mq.cs?` is optional it will only add it if doesn't already exist, so it will either use your existing MQ configuration
or configure your App to use the In Memory `BackgroundMqService` implementation.

Add `feature-mq` to your project with:

    $ mix feature-mq

![](https://raw.githubusercontent.com/ServiceStack/docs/master/docs/images/nav/feature-mq.png)

This will add the `TestMq` Service and make it available to your MQ endpoint. `TestMq` is a regular service that updates values in the 
App's registered `ICacheClient` and returns the Cache's current values as well as the internal Stats of the MQ:

```csharp
public class MqServices : Service
{
    public IMessageService MqService { get; set; }

    public void Any(PublishMq request)
    {
        PublishMessage(request.ConvertTo<TestMq>());
    }

    public object Any(TestMq request)
    {
        if (!string.IsNullOrEmpty(request.Name))
            Cache.Set("mq.name", request.Name);
        
        if (request.Add > 0)
            Cache.Increment("mq.counter", (uint)request.Add);
        else if (request.Add < 0)
            Cache.Decrement("mq.counter", (uint)(request.Add * -1));

        return new TestMqResponse {
            Name = Cache.Get<string>("mq.name"),
            Counter = Cache.Get<long>("mq.counter"),
            StatsDescription = MqService.GetStatsDescription(),
        };
    }
}
```

The 2 ways to call a MQ Service is directly using the `publish` or `sendOneWay` APIs (available in all ServiceStack Service Clients) where 
it send the request to the Service's `/oneway` endpoint which will automatically publish it to the registered MQ. 

Alternatively you can publish the Request DTO yourself from a different Service Implementation as done in `PublishMq`, as-is typical for
Services that queues sending emails without blocking Service Execution.

The feature's UI allows you to publish `TestMq` messages using either approach:

```js
client = new JsonServiceClient('/');

var oneway = document.querySelector('input[name=mq-publish]:checked').value === "OneWay";
if (oneway) {
    client.publish(new TestMq({ name: $txtName.value, add: parseInt(add) }))
} else {
    client.post(new PublishMq({ name: $txtName.value, add: parseInt(add) }))
}
```

Both approaches end with the same result with the `TestMq` Request DTO published and executed by the registered MQ Service as shown in the
UI which is periodically updated with the current state in the Cache and the internal stats of the MQ Service showing how many messages it processed.

### feature-authrepo

Another UI feature `mix` available is a UI to browse and search for registered users in an Auth Repository.

This wasn't generically possible before as `IAuthRepository` didn't previously provide any API's to be able to query all Users, 
which is now available in the new `IQueryUserAuth` API:

```csharp
public interface IQueryUserAuth
{
    List<IUserAuth> GetUserAuths(string orderBy = null, int? skip = null, int? take = null);
    List<IUserAuth> SearchUserAuths(string query, string orderBy = null, int? skip = null, int? take = null);
}
```

This is now implemented in all ServiceStack Auth Repositories although there are limitations depending on the queryability of the underlying data provider.

Searching in these Auth Repositories are efficient and searches in **UserName**, **Email**, **DisplayName** and **Company** fields:

 - `OrmLiteAuthRepository`
 - `InMemoryAuthRepository` 
 - `MongoDbAuthRepository` 

For RavenDB it reuses the existing Username/Email indexes so only searches **UserName**, **Email** fields and only performs a StartsWith/EndsWith 
search as allowed by RavenDB:

 - `RavenDbUserAuthRepository` 

Searches and Order By's are very inefficient in Redis as it needs to deserialize all users to perform the querying/sorting on the client.
Just paging through users with skip/take is efficient as it only needs to deserialize the partial resultset.

 - `RedisAuthRepository`

All queries performs a table scan in DynamoDB but searches all fields:

 - `DynamoDbAuthRepository`

#### API Usage

These API's are accessible from an `IAuthRepository` dependency, if you're using a custom Auth Repository it will need to implement 
`IQueryUserAuth` otherwise calling these APIs (and feature) will throw a `NotSupportedException`:

```csharp
AuthRepository.GetUserAuths(orderBy:fieldName, skip:skip, take:take)
AuthRepository.SearchUserAuths(query:q, orderBy:fieldName, skip:skip, take:take)
```

The `orderBy` is the field name you want to order the results by, e.g. `UserName` and can suffixed with the `DESC` modifier to order 
results in descending order, e.g. `UserName DESC`.

In `#Script` these API's are available in `camelCase` off `authRepo` using a JS Object literal as seen in `users.html` page usage of this feature:

```hbs
{% raw %}{{ authRepo.searchUserAuths({ query:qs.q, take: pageSize, skip: pageSize*page }) | to => users }}{% endraw %}
```

#### Users UI

Clicking the **Users** menu item will show you a list of searchable and pageable registered Users in a summary view:

![](https://raw.githubusercontent.com/ServiceStack/docs/master/docs/images/mix/feature-authrepo.png)

Clicking on a user will show you a complete list of fields stored for that user, including any custom fields, if you're using a Custom
`UserAuth` table:

![](https://raw.githubusercontent.com/ServiceStack/docs/master/docs/images/mix/feature-authrepo-admin.png)
