# 🐦 Tweeter

A full-featured Twitter clone built with **Clean Architecture** principles using **ASP.NET Core 9**, **Entity Framework Core**, and **SignalR**. This project demonstrates modern software architecture patterns, real-time communication, and best practices in enterprise application development.

![.NET](https://img.shields.io/badge/.NET-9.0-512BD4?logo=dotnet)
![C#](https://img.shields.io/badge/C%23-12.0-239120?logo=csharp)
![SignalR](https://img.shields.io/badge/SignalR-Real--time-00ADD8)
![Clean Architecture](https://img.shields.io/badge/Clean-Architecture-brightgreen)
![Entity Framework](https://img.shields.io/badge/EF_Core-9.0-512BD4)

## ✨ Features

### 🔐 **Authentication & Authorization**
- JWT-based authentication
- ASP.NET Core Identity integration
- External login providers (Google)
- Role-based authorization
- Email verification system

### 📱 **Community Features**
- ✅ **Tweets**: Create, update, delete tweets with image support
- ✅ **Retweets**: Share tweets with optional comments
- ✅ **Likes**: Like tweets and retweets
- ✅ **Mentions**: Tag users in tweets (@username)
- ✅ **Hashtags**: Categorize tweets with #hashtags
- ✅ **Replies**: Comment on tweets
- ✅ **Timeline**: View personalized feed from followed users

### 👥 **Social Networking**
- Follow/unfollow users
- View followers and following lists
- Get follower/following counts
- Check follow status between users

### 💬 **Real-time Chat**
- One-on-one messaging with SignalR
- Real-time message delivery
- Online/offline status tracking
- Chat history persistence

### 🔔 **Notifications**
- Real-time notifications via SignalR Hub
- Activity notifications (likes, retweets, follows, mentions)
- Push notifications support

## 🏗️ Architecture

This project follows **Clean Architecture** (Onion Architecture) principles, ensuring:
- ✅ **Separation of Concerns**
- ✅ **Dependency Inversion**
- ✅ **Testability**
- ✅ **Maintainability**
- ✅ **Technology Independence**

### Project Structure

```
Tweeter/
├── Tweeter.APIs/                      # 🌐 Presentation Layer (Web API)
│   ├── Program.cs                     # Application entry point
│   ├── Extensions/                    # Service registrations
│   ├── Middlewares/                   # Custom middlewares
│   └── wwwroot/                       # Static files (images)
│
├── Tweeter.Apis.Controllers/          # 🎮 API Controllers
│   └── Controllers/
│       ├── Community/                 # Tweet management endpoints
│       ├── Following/                 # Follow/unfollow endpoints
│       ├── Identity/                  # Authentication endpoints
│       └── Messages/                  # Chat endpoints
│
├── Tweeter.Core.Application/          # 💼 Application Layer (Business Logic)
│   ├── Features/                      # CQRS Features
│   │   ├── Community/                 # Tweet commands & queries
│   │   ├── Following/                 # Follow/unfollow commands
│   │   ├── Identity/                  # Auth commands & queries
│   │   └── Messages/                  # Chat queries
│   ├── Services/                      # Application services
│   │   ├── Hubs/                      # SignalR hubs
│   │   │   ├── ChatHub.cs             # Real-time chat
│   │   │   ├── NotificationHub.cs     # Real-time notifications
│   │   │   └── CommunityHub.cs        # Real-time tweets
│   │   └── Identity/                  # Identity services
│   ├── Bases/                         # Base classes
│   └── Mappings/                      # AutoMapper profiles
│
├── Tweeter.Core.Application.Abstraction/  # 📝 Interfaces & DTOs
│   ├── Dtos/                          # Data Transfer Objects
│   └── Services/                      # Service interfaces
│
├── Tweeter.Core.Domain/               # 🎯 Domain Layer (Entities)
│   ├── Entities/
│   │   ├── Identity/                  # User entities
│   │   │   └── ApplicationUser.cs
│   │   └── Data/                      # Business entities
│   │       ├── Tweet.cs               # Tweet entity
│   │       ├── Retweet.cs             # Retweet entity
│   │       ├── Like.cs                # Like entity
│   │       ├── Follow.cs              # Follow relationship
│   │       ├── Message.cs             # Chat message
│   │       ├── Hashtag.cs             # Hashtag entity
│   │       └── Mention.cs             # Mention entity
│   ├── Common/                        # Base entities
│   └── AppMateData/                   # App metadata & routing
│
├── Tweeter.Infrastructure.Persistence/   # 🗄️ Data Access Layer
│   ├── _Context/                      # DbContext
│   ├── _Data/                         # Migrations
│   ├── Repositories/                  # Repository implementations
│   └── UnitOfWork/                    # Unit of Work pattern
│
├── Tweeter.Infrastructure/            # 🔧 Infrastructure Services
│   ├── Services/                      # External services
│   │   ├── EmailService/              # Email sending
│   │   ├── AttachmentService/         # File uploads
│   │   └── Cache/                     # Redis caching
│   └── External/                      # External integrations
│
├── Tweeter.Shared/                    # 📦 Shared Library
│   └── Results/                       # Result & Response types
│
└── ExternalLogins/                    # 🔐 OAuth Demo Project
```

### Architecture Layers

```
┌─────────────────────────────────────────┐
│      Presentation Layer (APIs)          │
│   Controllers, Middlewares, SignalR     │
└──────────────┬──────────────────────────┘
               │
┌──────────────▼──────────────────────────┐
│      Application Layer (Use Cases)      │
│   Commands, Queries, Services, Hubs     │
└──────────────┬──────────────────────────┘
               │
┌──────────────▼──────────────────────────┐
│      Domain Layer (Business Logic)      │
│     Entities, Value Objects, Rules      │
└──────────────────────────────────────────┘
               ▲
┌──────────────┴──────────────────────────┐
│   Infrastructure Layer (Data & Services)│
│  DbContext, Repositories, External APIs │
└─────────────────────────────────────────┘
```

## 🚀 Getting Started

### Prerequisites

- **.NET SDK 9.0** or higher
- **SQL Server** (LocalDB or full version)
- **Redis** (optional, for caching)
- **Visual Studio 2022** / **VS Code** / **Rider**

### Installation

1. **Clone the repository**
```bash
git clone https://github.com/01124833532mo/Tweeter.git
cd Tweeter
```

2. **Restore dependencies**
```bash
dotnet restore
```

3. **Update database connection string**

Edit `appsettings.json` in `Tweeter.APIs`:
```json
{
  "ConnectionStrings": {
    "DefaultConnection": "Server=(localdb)\\mssqllocaldb;Database=TweeterDb;Trusted_Connection=True;"
  }
}
```

4. **Apply migrations**
```bash
cd Tweeter.APIs
dotnet ef database update --project ../Tweeter.Infrastructure.Persistence
```

5. **Run the application**
```bash
dotnet run --project Tweeter.APIs
```

6. **Access the API**
- Swagger UI: `https://localhost:5001/swagger`
- API Base URL: `https://localhost:5001/api`

## 📡 API Endpoints

### Authentication
```
POST   /api/Authentication/Register      # Register new user
POST   /api/Authentication/Login         # Login user
POST   /api/Authentication/RefreshToken  # Refresh JWT token
POST   /api/Authentication/ConfirmEmail  # Verify email
POST   /api/Authentication/ResetPassword # Reset password
```

### Community (Tweets)
```
POST   /api/Community/CreateTweet        # Create new tweet
GET    /api/Community/GetAllTweets       # Get all tweets
GET    /api/Community/GetTweetsForFollowedUsers  # Get timeline
GET    /api/Community/{id}               # Get tweet by ID
PUT    /api/Community/Update/{id}        # Update tweet
DELETE /api/Community/Delete/{id}        # Delete tweet

POST   /api/Community/Like/{id}          # Like tweet
POST   /api/Community/Retweet/{id}       # Retweet with comment
DELETE /api/Community/UnRetweet/{id}     # Delete retweet
POST   /api/Community/LikeRetweet/{id}   # Like a retweet
```

### Following
```
POST   /api/Following/FollowUser         # Follow user
DELETE /api/Following/UnfollowUser       # Unfollow user
GET    /api/Following/GetFollowers       # Get followers list
GET    /api/Following/GetFollowing       # Get following list
GET    /api/Following/GetCountOfFollowers  # Get followers count
GET    /api/Following/GetCountOfFollowing  # Get following count
GET    /api/Following/IsFollowing        # Check follow status
```

### Messages (Chat)
```
GET    /api/Messages/GetChatHistory      # Get chat messages
GET    /api/Messages/GetChatsList        # Get all conversations
```

## 🔌 SignalR Hubs

### Chat Hub (`/hubs/chat`)
Real-time one-on-one messaging:
```csharp
// Connect
OnConnectedAsync()

// Send message
SendMessage(string receiverId, string content)

// Disconnect
OnDisconnectedAsync()
```

### Notification Hub (`/hubs/notification`)
Real-time notifications for user activities.

### Community Hub (`/hubs/community`)
Real-time tweet updates:
```csharp
SendTweet(CreateTweetDto)
UpdateTweet(int tweetId, UpdateTweetDto)
DeleteTweet(int tweetId)
LikeTweet(int tweetId)
Retweet(int tweetId, string? comment)
```

## 🎯 Design Patterns Used

- ✅ **CQRS** (Command Query Responsibility Segregation) with MediatR
- ✅ **Repository Pattern** for data access
- ✅ **Unit of Work Pattern** for transaction management
- ✅ **Dependency Injection** throughout all layers
- ✅ **Mediator Pattern** for command/query handling
- ✅ **Result Pattern** for error handling
- ✅ **DTOs** for data transfer
- ✅ **AutoMapper** for object mapping
- ✅ **Fluent Validation** for input validation

## 🔧 Technologies & Libraries

### Backend
- **ASP.NET Core 9.0** - Web API framework
- **Entity Framework Core 9.0** - ORM
- **SQL Server** - Database
- **SignalR** - Real-time communication
- **MediatR** - CQRS implementation
- **AutoMapper** - Object mapping
- **FluentValidation** - Input validation
- **MailKit** - Email sending
- **JWT Bearer** - Authentication
- **Swashbuckle** - Swagger/OpenAPI

### Infrastructure
- **Redis** (StackExchange.Redis) - Caching
- **Identity** - User management
- **OAuth 2.0** - External authentication

## 📦 NuGet Packages

```xml
<!-- Key Dependencies -->
<PackageReference Include="Microsoft.EntityFrameworkCore.SqlServer" Version="9.0.4" />
<PackageReference Include="Microsoft.AspNetCore.SignalR.Client.Core" Version="9.0.4" />
<PackageReference Include="Microsoft.AspNetCore.Authentication.JwtBearer" Version="9.0.4" />
<PackageReference Include="MediatR" Version="12.5.0" />
<PackageReference Include="AutoMapper" Version="14.0.0" />
<PackageReference Include="FluentValidation" Version="11.11.0" />
<PackageReference Include="MailKit" Version="4.11.0" />
<PackageReference Include="StackExchange.Redis" Version="2.8.41" />
```

## 🔐 Security Features

- **JWT Token Authentication** with refresh tokens
- **Password hashing** with ASP.NET Core Identity
- **Email verification** for new accounts
- **Role-based authorization**
- **CORS configuration** for frontend integration
- **HTTPS enforcement**
- **Data validation** with FluentValidation
- **SQL injection protection** via EF Core

## 🧪 Testing

### Example: Testing Tweet Creation
```csharp
[Fact]
public async Task CreateTweet_ShouldReturnSuccess_WhenValid()
{
    // Arrange
    var command = new CreateTweetCommand
    {
        Content = "Hello World!",
        ImageUrl = null
    };

    // Act
    var result = await _mediator.Send(command);

    // Assert
    Assert.True(result.Succeeded);
    Assert.NotNull(result.Data);
}
```

## 🚧 Future Enhancements

- [ ] **Trending Topics** algorithm
- [ ] **Advanced Search** (users, tweets, hashtags)
- [ ] **Media Uploads** (videos, GIFs)
- [ ] **Stories** feature
- [ ] **Direct Message Groups**
- [ ] **Tweet Analytics**
- [ ] **Bookmark** feature
- [ ] **Lists** functionality
- [ ] **Polls** in tweets
- [ ] **Mobile App** (React Native / MAUI)
- [ ] **GraphQL API** support
- [ ] **Elasticsearch** for advanced search
- [ ] **Docker** containerization
- [ ] **Kubernetes** deployment
- [ ] **Unit & Integration Tests**

## 📚 Learning Resources

This project demonstrates:
- Clean Architecture implementation in .NET
- CQRS with MediatR
- Real-time communication with SignalR
- Entity Framework Core advanced features
- JWT authentication & authorization
- Repository and Unit of Work patterns
- Dependency Injection best practices

## 🤝 Contributing

Contributions are welcome! To contribute:

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

### Contribution Guidelines
- Follow Clean Architecture principles
- Write meaningful commit messages
- Add XML documentation to public APIs
- Ensure all tests pass
- Update README if adding new features

## 📄 License

This project is open source and available under the [MIT License](LICENSE).

## 👨‍💻 Author

**01124833532mo**
- GitHub: [@01124833532mo](https://github.com/01124833532mo)
- Forked from: [@Mahmoud-Ahmed-23/Tweeter](https://github.com/Mahmoud-Ahmed-23/Tweeter)

## 🙏 Acknowledgments

- **Clean Architecture** by Robert C. Martin
- **Microsoft .NET** team for excellent documentation
- **ASP.NET Core** community
- Original repository by **Mahmoud-Ahmed-23**

## 📞 Support

- **Issues**: [GitHub Issues](https://github.com/01124833532mo/Tweeter/issues)
- **Discussions**: [GitHub Discussions](https://github.com/01124833532mo/Tweeter/discussions)

---

⭐ **Star this repository** if you found it helpful!

💡 **Have questions?** Open an issue or start a discussion!

📖 **Want to learn more?** Check out the [Clean Architecture documentation](https://blog.cleancoder.com/uncle-bob/2012/08/13/the-clean-architecture.html)

---

**Built with ❤️ using Clean Architecture principles and .NET 9**
