
#### Add pacote:
```
	dotnet add 'projeto'.csproj package Swashbuckle.AspNetCore -v 5.0.0

	dotnet add package Microsoft.AspNetCore.StaticFiles --version 2.2.0
```

#### No arquivo Startup.cs adicionar:	
```
	using Microsoft.OpenApi.Models;
```

###### Metodo ConfigureServices:
```
services.AddSwaggerGen(c =>
{
      c.SwaggerDoc("v1", new OpenApiInfo { Title = "My API", Version = "v1" });
});
```

###### Metodo Configure para todos os ambientes:
```
app.UseSwagger();

app.UseSwaggerUI(c =>
{
    c.SwaggerEndpoint("./swagger/v1/swagger.json", "My API V1");
    c.RoutePrefix = string.Empty;
});

```

###### Metodo Configure somente para ambiente de desenvolvimento:
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

