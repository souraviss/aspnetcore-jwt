# aspnetcore-jwt
ASP.Net Core JWT to assist with JWT authentication/authorization for Web API when using Entity Framework Core Identity

## Build Status
[![Build status](https://saji.visualstudio.com/Open%20Source/_apis/build/status/aspnetcore-jwt-import)](https://saji.visualstudio.com/Open%20Source/_build/latest?definitionId=24)

## Dependencies
- ASP.Net Core 2.1
  - Microsoft.AspNetCore.Authentication.JwtBearer
  - System.IdentityModel.Tokens.Jwt

## Quickstart
- Install NuGet package
- Initialize JWT in `Startup.ConfigureServices`.  For example ([Sampe Startup](/sample/AspNetCore.Jwt.Sample/Startup.cs)):
```
services.AddJwtBearerAuthentication(
    Configuration["Authentication:TokenSigningKey"],
    Configuration["Authentication:Issuer"],
    Configuration["Authentication:Audience"],
    60,
    1440);
```
- Inject `TokenBuilder` class into appropriate controller or class (`AddJwtBearerAuthentication` creates transient dependency rule for this class)
-- The `GenerateToken` method creates a JWT signing token

## Authorization
The [BaseAuthorizationHandler](/src/AspNetCore.Jwt/BaseAuthorizationHandler.cs) abstrat class assists with the authorization policies.

It collects the various segments of the API URL so that you can validate them against authenticated user's claims.

See the [OwnUserHandler](/sample/AspNetCore.Jwt.Sample/Logic/OwnUserHandler.cs) in the sample code for an example implementation.