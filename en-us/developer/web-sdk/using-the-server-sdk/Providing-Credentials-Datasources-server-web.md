## Providing Credentials to Data Sources

### Overview

The Server SDK allows you to pass in a set of credentials to be used
when accessing the data source.

### Code

The first step is to implement
__IRVAuthenticationProvider__
and return it as the
__AuthenticationProvider__
property in
__IRevealSdkContext__,
as shown below.

``` csharp
public class EmbedAuthenticationProvider : IRVAuthenticationProvider
{
    public Task<IRVDataSourceCredential> ResolveCredentialsAsync(string userId, RVDashboardDataSource dataSource)
        {
            IRVDataSourceCredential userCredential = null;
            if (dataSource is RVPostgresDataSource)
            {
                userCredential = new RVUsernamePasswordDataSourceCredential("postgresuser", "password");
            }
            else if (dataSource is RVSqlServerDataSource)
            {
                userCredential = new RVUsernamePasswordDataSourceCredential("sqlserveruser", "password", "domain");
            }
            else if (dataSource is RVGoogleDriveDataSource)
            {
                userCredential = new RVBearerTokenDataSourceCredential("fhJhbUci0mJSUzi1nIiSint....", "user@company.com");
            }
            else if (dataSource is RVRestDataSource)
            {
                userCredential = new RVUsernamePasswordDataSourceCredential(); // Anonymous
            }
            return Task.FromResult<IRVDataSourceCredential>(userCredential);
    }
}
```

### Choosing Which Class to Implement

There are two classes that can be used, both implementing the
__IRVDataSourceCredential__
interface. You need to choose the class depending on your data source,
as detailed below.

  - Class
    __RVBearerTokenDataSourceCredential__
    works with:

      - Analytics tools (Google Analytics).

      - Content Managers and Cloud Services (Box, Dropbox, Google Drive,
        OneDrive and SharePoint Online).

  - Class
    __RVUsernamePasswordDataSourceCredential__
    works with:

      - Customer Relationship Managers (Microsoft Dynamics CRM
        On-Premises and Online)

      - Databases (Microsoft SQL Server, Microsoft Analysis Services
        Server, MySQL, PostgreSQL, Oracle, Sybase)

  - **Both classes** work with:

      - Other Data Sources (OData Feed, Web Resources, REST API).

### No Authentication

Sometimes you might work with an anonymous resource, without
authentication. In this particular case, you can use
__RVUsernamePasswordDataSourceCredential__,
which has an empty constructor. You can do this for any data source that
works with the class.

Code snippet to be used with the sample above:

``` csharp
else if (dataSource is RVRESTDataSource)
{
     userCredential = new RVUsernamePasswordDataSourceCredential();
}
```
### Related content

  - [Loading Dashboard Files](loading-dashboards-server-web.md)
  - [Replacing Data Sources](replacing-data-sources-server-web.md)
  - [In-Memory Data Support](in-memory-data-server-web.md)
  - [Providing Credentials to Data Sources (Desktop)](../../desktop-sdk/using-the-desktop-sdk/providing-credentials-datasources-desktop.md)