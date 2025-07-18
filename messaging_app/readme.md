# Building Robust APIs

## Project Overview

This project is a RESTful API for a messaging application built with Django and Django REST Framework. It allows users to participate in conversations and exchange messages with other users.

## Key Features

- User authentication and management
- Conversation creation and management
- Message sending and retrieval
- RESTful API endpoints for all operations

## Project Structure

```
messaging_app/
├── chats/                 # Main app for messaging functionality
│   ├── migrations/        # Database migrations
│   ├── models.py          # Data models (User, Conversation, Message)
│   ├── serializers.py     # Serializers for API data transformation
│   ├── views.py           # API viewset implementations
│   └── urls.py            # App-specific URL routing
├── messaging_app/         # Project configuration
│   ├── settings.py        # Django settings
│   └── urls.py            # Main URL routing
└── manage.py              # Django management script
```

## Installation & Setup

1. **Clone the repository**
   ```bash
   git clone https://github.com/MercyXp/alx-backend-python.git
   cd alx-backend-python/messaging_app
   ```

2. **Create and activate virtual environment**
   ```bash
   python -m venv venv
   source venv/bin/activate  # On Windows: venv\Scripts\activate
   ```

3. **Install dependencies**
   ```bash
   pip install -r requirements.txt
   ```

4. **Run migrations**
   ```bash
   python manage.py makemigrations
   python manage.py migrate
   ```

5. **Create superuser (optional)**
   ```bash
   python manage.py createsuperuser
   ```

6. **Run development server**
   ```bash
   python manage.py runserver
   ```

## API Endpoints

| Endpoint | Method | Description |
|----------|--------|-------------|
| `/api/users/` | GET, POST | List and create users |
| `/api/conversations/` | GET, POST | List and create conversations |
| `/api/conversations/{id}/` | GET, PUT, PATCH, DELETE | Retrieve, update, or delete a conversation |
| `/api/messages/` | GET, POST | List and create messages |
| `/api/messages/{id}/` | GET, PUT, PATCH, DELETE | Retrieve, update, or delete a message |

## Models

### User
- Extends Django's AbstractUser model
- Additional fields can be added as needed

### Conversation
- Tracks participants (many-to-many relationship with User)
- Has creation and update timestamps

### Message
- Belongs to a Conversation (foreign key)
- Has a sender (foreign key to User)
- Contains message content and timestamps

## Testing the API

You can test the API using tools like:
- Postman
- Swagger UI (if implemented)
- Django REST Framework's browsable API

## Project Objectives Achieved

- Scaffolded Django project with proper structure
- Implemented data models with relationships
- Created serializers for model instances
- Built API endpoints using DRF viewsets
- Configured URL routing
- Followed Django best practices

## Future Enhancements

1. Implement user authentication (JWT/OAuth)
2. Add message read receipts
3. Implement real-time messaging with WebSockets
4. Add file attachments to messages
5. Implement message search functionality

## Author

Mercy Munzenzi

ALX ProDev Backend Program  
18th July, 2025.