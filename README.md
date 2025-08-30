# 🚀 APIFuncional

Uma API RESTful moderna desenvolvida em ASP.NET Core 8.0 com autenticação JWT e gerenciamento de produtos.

## 📋 Sobre o Projeto

O **APIFuncional** é uma API completa que demonstra as melhores práticas de desenvolvimento com ASP.NET Core, incluindo:

- 🔐 **Autenticação e Autorização** com JWT (JSON Web Tokens)
- 👥 **Gerenciamento de Usuários** com ASP.NET Core Identity
- 📦 **CRUD de Produtos** com validações e tratamento de erros
- 🗄️ **Entity Framework Core** com SQL Server
- 📚 **Swagger/OpenAPI** para documentação interativa
- 🔒 **CORS** configurado para desenvolvimento e produção
- ✅ **Validações** robustas com Data Annotations

## 🛠️ Tecnologias Utilizadas

- **.NET 8.0** - Framework principal
- **ASP.NET Core Web API** - Para criação da API REST
- **Entity Framework Core 8.0.19** - ORM para acesso a dados
- **SQL Server** - Banco de dados
- **ASP.NET Core Identity** - Sistema de autenticação e autorização
- **JWT Bearer Authentication** - Autenticação baseada em tokens
- **Swashbuckle.AspNetCore** - Documentação Swagger/OpenAPI
- **CORS** - Cross-Origin Resource Sharing

## 📁 Estrutura do Projeto

```
APIFuncional/
├── Controllers/           # Controladores da API
│   ├── AuthController.cs  # Autenticação e registro
│   └── ProdutosController.cs # CRUD de produtos
├── Models/               # Modelos de dados
│   ├── Produto.cs
│   ├── LoginUserViewModel.cs
│   ├── RegisterUserViewModel.cs
│   └── JwtSettings.cs
├── Configuration/        # Configurações da aplicação
│   ├── ApiConfig.cs
│   ├── CorsConfig.cs
│   ├── DbContextConfig.cs
│   ├── IdentityConfig.cs
│   └── SwaggerConfig.cs
├── Data/                 # Contexto do Entity Framework
├── Migrations/           # Migrações do banco de dados
└── Properties/           # Configurações do projeto
```

## 🚀 Como Executar o Projeto

### Pré-requisitos

- [.NET 8.0 SDK](https://dotnet.microsoft.com/download/dotnet/8.0)
- [SQL Server](https://www.microsoft.com/pt-br/sql-server/sql-server-downloads) (ou SQL Server Express)
- [Visual Studio 2022](https://visualstudio.microsoft.com/pt-br/) ou [Visual Studio Code](https://code.visualstudio.com/)

### Passos para Execução

1. **Clone o repositório**
   ```bash
   git clone https://github.com/seu-usuario/APIFuncional.git
   cd APIFuncional
   ```

2. **Configure a string de conexão**
   
   Edite o arquivo `APIFuncional/appsettings.json` e ajuste a string de conexão:
   ```json
   {
     "ConnectionStrings": {
       "DefaultConnection": "Server=localhost\\SQLEXPRESS;Database=ApiFuncional;Trusted_Connection=True;TrustServerCertificate=True;"
     }
   }
   ```

3. **Execute as migrações**
   ```bash
   cd APIFuncional
   dotnet ef database update
   ```

4. **Execute o projeto**
   ```bash
   dotnet run
   ```

5. **Acesse a documentação**
   
   Abra o navegador e acesse: `https://localhost:7001/swagger` ou `http://localhost:5001/swagger`

## 📖 Endpoints da API

### Autenticação (`/api/conta`)

- **POST** `/api/conta/registrar` - Registrar novo usuário
- **POST** `/api/conta/login` - Fazer login

### Produtos (`/api/produtos`) - Requer autenticação

- **GET** `/api/produtos` - Listar todos os produtos
- **GET** `/api/produtos/{id}` - Buscar produto por ID
- **POST** `/api/produtos` - Criar novo produto
- **PUT** `/api/produtos/{id}` - Atualizar produto
- **DELETE** `/api/produtos/{id}` - Excluir produto

## 🔐 Autenticação

A API utiliza JWT (JSON Web Tokens) para autenticação. Para acessar endpoints protegidos:

1. Registre-se ou faça login usando os endpoints de autenticação
2. Use o token JWT retornado no header `Authorization: Bearer {token}`

### Exemplo de uso:

```bash
# Login
curl -X POST "https://localhost:7001/api/conta/login" \
     -H "Content-Type: application/json" \
     -d '{"email": "usuario@exemplo.com", "password": "Senha123!"}'

# Usar o token retornado
curl -X GET "https://localhost:7001/api/produtos" \
     -H "Authorization: Bearer {seu-token-jwt}"
```

## 📝 Modelos de Dados

### Produto
```json
{
  "id": 1,
  "nome": "Produto Exemplo",
  "preco": 99.99,
  "quantidadeEstoque": 10,
  "descricao": "Descrição do produto"
}
```

### Registro de Usuário
```json
{
  "email": "usuario@exemplo.com",
  "password": "Senha123!",
  "confirmPassword": "Senha123!"
}
```

### Login
```json
{
  "email": "usuario@exemplo.com",
  "password": "Senha123!"
}
```

## ⚙️ Configurações

### JWT Settings (appsettings.json)
```json
{
  "JwtSettings": {
    "Segredo": "SUA_CHAVE_SECRETA_AQUI_MUITO_LONGA_E_SEGURA",
    "Emissor": "APIFuncional",
    "Audiencia": "https://localhost",
    "ExpiracaoHoras": 2
  }
}
```

## 🔧 Possíveis Melhorias

### Funcionalidades
- [ ] **Logs estruturados** com Serilog
- [ ] **Cache** com Redis ou Memory Cache
- [ ] **Paginação** nos endpoints de listagem
- [ ] **Filtros e busca** avançada
- [ ] **Upload de imagens** para produtos
- [ ] **Categorias de produtos**
- [ ] **Sistema de avaliações**
- [ ] **Relatórios** e analytics

### Segurança
- [ ] **Rate limiting** para prevenir abuso
- [ ] **Refresh tokens** para renovação automática
- [ ] **Validação de senha forte**
- [ ] **Confirmação de email**
- [ ] **Recuperação de senha**
- [ ] **Auditoria** de ações dos usuários

### Performance
- [ ] **Compressão** de respostas
- [ ] **Async/await** em todas as operações de I/O
- [ ] **Connection pooling** otimizado
- [ ] **Índices** no banco de dados
- [ ] **Lazy loading** para relacionamentos

### Arquitetura
- [ ] **Repository Pattern** para abstração de dados
- [ ] **Unit of Work** para transações
- [ ] **AutoMapper** para mapeamento de objetos
- [ ] **FluentValidation** para validações complexas
- [ ] **MediatR** para CQRS
- [ ] **Health Checks** para monitoramento

### DevOps
- [ ] **Docker** para containerização
- [ ] **CI/CD** com GitHub Actions
- [ ] **Testes unitários** e de integração
- [ ] **Code coverage** reports
- [ ] **Static code analysis**

## 🤝 Contribuindo

1. Faça um fork do projeto
2. Crie uma branch para sua feature (`git checkout -b feature/AmazingFeature`)
3. Commit suas mudanças (`git commit -m 'Add some AmazingFeature'`)
4. Push para a branch (`git push origin feature/AmazingFeature`)
5. Abra um Pull Request

## 📄 Licença

Este projeto está sob a licença MIT. Veja o arquivo [LICENSE](LICENSE) para mais detalhes.

## 👨‍💻 Autor

**Seu Nome**
- GitHub: [@RodJunio94](https://github.com/RodJunio94)
- LinkedIn: [Junio Rodrigues](https://www.linkedin.com/in/junio-santos-rodrigues/)

## 🙏 Agradecimentos

- [Microsoft](https://microsoft.com) pelo ASP.NET Core
- [Entity Framework](https://docs.microsoft.com/en-us/ef/) pela documentação
- Comunidade .NET por todo o suporte

---

⭐ Se este projeto te ajudou, considere dar uma estrela no repositório!
