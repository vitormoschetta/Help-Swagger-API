
## Add pacote:
```
	dotnet add 'projeto'.csproj package Swashbuckle.AspNetCore -v 5.0.0

	dotnet add package Microsoft.AspNetCore.StaticFiles --version 2.2.0
```

## No arquivo Startup.cs adicionar:	
```
	using Microsoft.OpenApi.Models;
```

## Metodo ConfigureServices:

#### Apenas a Ferramenta de Documentação
```
services.AddSwaggerGen(c =>
{
      c.SwaggerDoc("v1", new OpenApiInfo
	{
	    Version = "v1",
	    Title = "API",
	    Description = "A simple example ASP.NET Core Web API",
	    Contact = new OpenApiContact
	    {
		Name = "Vitor Moschetta",
		Email = "vitormoschetta@gmail.com"
	    }
	});
});
```

#### Ferramenta de Documentação + Metodo de Autorização Bearer:
```
services.AddSwaggerGen(c =>
{
	c.SwaggerDoc("v1", new OpenApiInfo
	{
	    Version = "v1",
	    Title = "API",
	    Description = "A simple example ASP.NET Core Web API",
	    Contact = new OpenApiContact
	    {
		Name = "Vitor Moschetta",
		Email = "vitormoschetta@gmail.com"
	    }
	});
	c.AddSecurityDefinition("Bearer", new OpenApiSecurityScheme
	{
	    Description = @"Cabeçalho de autorização JWT usando o esquema Bearer.  
			Digite 'Bearer' [espaço] em seguida, seu token na entrada de texto abaixo.
			Exemplo: 'Bearer 12345abcdef'",
	    Name = "Authorization",
	    In = ParameterLocation.Header,
	    Type = SecuritySchemeType.ApiKey,
	    Scheme = "Bearer"
	});
	c.AddSecurityRequirement(new OpenApiSecurityRequirement()
	{
	    {
	    new OpenApiSecurityScheme
	    {
		Reference = new OpenApiReference
		{
		    Type = ReferenceType.SecurityScheme,
		    Id = "Bearer"
		},
		Scheme = "oauth2",
		Name = "Bearer",
		In = ParameterLocation.Header,

		},
		new List<string>()
	    }
	}); 
});
```

## Metodo Configure para todos os ambientes:
```
app.UseSwagger();

app.UseSwaggerUI(c =>
{
    c.SwaggerEndpoint("./swagger/v1/swagger.json", "My API V1");
    c.RoutePrefix = string.Empty;
});

```

## Metodo Configure somente para ambiente de desenvolvimento:
```
app.UseSwagger();

app.UseSwaggerUI(c =>
{
    c.SwaggerEndpoint("/swagger/v1/swagger.json", "My API V1");
    c.RoutePrefix = string.Empty;
});

```



Pronto, basta executar a aplicação que a pagina inicial do Swagger irá aparecer, com o seu projeto
modelado, mostrando os métodos e tipos de solicitação http.

Você poderá executar/testar sua api ao mesmo tempo que a documenta.

Lembrando que o Swagger só funciona em ambiente de desenvolvimento.

