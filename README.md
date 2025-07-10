# 🌐 Django Social Network

A comprehensive social media platform built with Django 5.2, featuring user authentication, friend connections, post management, real-time notifications, and advanced moderation capabilities.

## 📋 Table of Contents

- [Features](#-features)
- [Database Schema](#-database-schema)
- [System Architecture](#-system-architecture)
- [Technology Stack](#-technology-stack)
- [Project Structure](#-project-structure)
- [Installation & Setup](#-installation--setup)
- [Configuration](#-configuration)
- [Usage Guide](#-usage-guide)
- [API Endpoints](#-api-endpoints)
- [User Roles & Permissions](#-user-roles--permissions)
- [Security Features](#-security-features)
- [Development](#-development)
- [Deployment](#-deployment)
- [Contributing](#-contributing)
- [License](#-license)

## ✨ Features

### 🔐 Authentication & User Management

- **Custom User Model**: Extended Django's AbstractUser with additional profile fields
- **User Registration**: Secure signup with automatic group assignment
- **Profile Management**: Customizable profiles with bio, profile pictures, birthday, and location
- **Account Security**: Ban/unban functionality for moderators

### 👥 Social Features

- **Friend System**: Send, accept, decline, and cancel friend requests
- **Friend Suggestions**: Intelligent friend recommendations
- **User Search**: Find users across the platform
- **Friends List**: View and manage friend connections

### 📝 Content Management

- **Post Creation**: Rich text posts with visibility controls
- **Post Visibility**: Public, Friends-only, or Private posts
- **Post Interactions**: Like/unlike posts with real-time counters
- **Comments System**: Threaded comments on posts
- **Content Moderation**: Edit and delete own content

### 🔔 Notification System

- **Real-time Notifications**: Friend requests, likes, comments
- **Notification Management**: Mark as read, delete individual or all notifications
- **Notification Counter**: Live count of unread notifications

### 🛡️ Moderation & Administration

- **Moderator Dashboard**: Dedicated interface for content moderation
- **User Management**: Ban/unban users, delete posts
- **Permission System**: Role-based access control
- **Content Oversight**: Delete any post, manage user accounts

### 🎨 User Experience

- **Responsive Design**: Mobile-friendly interface
- **Clean UI**: Modern, intuitive user interface
- **Easy Navigation**: Streamlined user flows
- **Explore Page**: Discover new content and users

## 🗄️ Database Schema

The application uses five main models to handle users, posts, comments, friend relationships, and notifications:

### Core Models

**CustomUser**: Extended Django user model with profile fields like bio, profile picture, birthday, and location. Includes a ban status for moderation.

**Post**: User-generated content with visibility settings (public, friends-only, private). Tracks likes and has a relationship to comments.

**Comment**: Allows users to comment on posts. Each comment is linked to both a post and the user who wrote it.

**FriendRequest**: Manages friend relationships between users. Tracks who sent the request, who received it, and whether it was accepted.

**Notification**: Real-time notifications for user interactions like friend requests, likes, and comments. Can be marked as read or deleted.

## 🏗️ System Architecture

The project is organized into two main Django apps plus configuration:

**Main Project (social_network/)**: Contains Django settings, URL routing, and deployment configuration.

**Users App (users/)**: Handles user authentication, profiles, and account management. Includes custom user model with additional profile fields.

**Network App (network/)**: Manages all social features including posts, comments, friend requests, and notifications.

**Templates & Static Files**: Frontend templates using Django's template system, CSS styling, and JavaScript for interactivity.

**Media Storage**: User-uploaded files like profile pictures are stored in the media directory.

## 🛠️ Technology Stack

### Backend

- **Framework**: Django 5.2.3
- **Database**: SQLite (development) / PostgreSQL (production ready)
- **Authentication**: Django's built-in auth system with custom user model
- **File Handling**: Pillow for image processing
- **Timezone**: Django timezone utilities

### Frontend

- **Templates**: Django Template Language
- **Styling**: CSS3 with custom stylesheets
- **JavaScript**: Vanilla JS for interactivity
- **Responsive**: Mobile-first design approach

### Development Tools

- **ASGI/WSGI**: Production-ready deployment interfaces
- **Admin Interface**: Django Admin with custom configurations
- **Migrations**: Django's migration system
- **Static Files**: Django's static file handling

## 📁 Project Structure

```
social_network/
├── 📄 manage.py                    # Django management script
├── 📄 requirements.txt             # Python dependencies
├── 📄 db.sqlite3                   # SQLite database
├── 📄 README.md                    # This file
│
├── 📁 social_network/              # Main project configuration
│   ├── __init__.py
│   ├── settings.py                 # Django settings
│   ├── urls.py                     # Root URL configuration
│   ├── wsgi.py                     # WSGI configuration
│   └── asgi.py                     # ASGI configuration
│
├── 📁 users/                       # User management app
│   ├── __init__.py
│   ├── admin.py                    # Admin configurations
│   ├── apps.py                     # App configuration
│   ├── models.py                   # CustomUser model
│   ├── views.py                    # Authentication views
│   ├── forms.py                    # User forms
│   ├── urls.py                     # User URL patterns
│   ├── signals.py                  # User-related signals
│   ├── middleware.py               # Custom middleware
│   ├── tests.py                    # Unit tests
│   ├── migrations/                 # Database migrations
│   └── templates/users/            # User templates
│
├── 📁 network/                     # Social networking app
│   ├── __init__.py
│   ├── admin.py                    # Admin configurations
│   ├── apps.py                     # App configuration
│   ├── models.py                   # Social models
│   ├── views.py                    # Social networking views
│   ├── forms.py                    # Post/comment forms
│   ├── urls.py                     # Network URL patterns
│   ├── signals.py                  # Notification signals
│   ├── context_processors.py       # Custom context processors
│   ├── tests.py                    # Unit tests
│   ├── migrations/                 # Database migrations
│   └── templates/network/          # Network templates
│       ├── welcome.html            # Landing page
│       ├── post_list.html          # Main feed
│       ├── profile.html            # User profiles
│       ├── post_detail.html        # Individual posts
│       ├── notifications.html      # Notifications page
│       ├── explore.html            # Explore page
│       ├── friend_suggestions.html # Friend suggestions
│       ├── mod_dashboard.html      # Moderator dashboard
│       └── partials/               # Reusable components
│
├── 📁 templates/                   # Global templates
│   ├── base.html                   # Base template
│   └── registration/               # Authentication templates
│       ├── login.html              # Login page
│       └── signup.html             # Registration page
│
├── 📁 static/                      # Static assets
│   ├── css/
│   │   └── styles.css              # Main stylesheet
│   └── js/
│       ├── main.js                 # Main JavaScript
│       └── moderator.js            # Moderator functions
│
└── 📁 media/                       # User uploaded files
    └── profiles/                   # Profile pictures
```

## 🚀 Installation & Setup

### Prerequisites

- Python 3.8+
- pip (Python package manager)
- Git

### Step-by-Step Installation

1. **Clone the Repository**

   ```bash
   git clone <repository-url>
   cd social_network
   ```

2. **Create Virtual Environment**

   ```bash
   python -m venv venv
   source venv/bin/activate  # On Windows: venv\Scripts\activate
   ```

3. **Install Dependencies**

   ```bash
   pip install -r requirements.txt
   ```

4. **Database Setup**

   ```bash
   python manage.py makemigrations
   python manage.py migrate
   ```

5. **Create Superuser**

   ```bash
   python manage.py createsuperuser
   ```

6. **Create User Groups**

   ```bash
   python manage.py shell
   ```

   ```python
   from django.contrib.auth.models import Group, Permission
   from django.contrib.contenttypes.models import ContentType
   from users.models import CustomUser
   from network.models import Post

   # Create groups
   regular_users = Group.objects.create(name='RegularUsers')
   moderators = Group.objects.create(name='Moderator')

   # Add permissions to moderators
   ban_permission = Permission.objects.get(codename='can_ban_users')
   delete_post_permission = Permission.objects.get(codename='can_delete_any_post')

   moderators.permissions.add(ban_permission, delete_post_permission)
   ```

7. **Collect Static Files** (for production)

   ```bash
   python manage.py collectstatic
   ```

8. **Run Development Server**

   ```bash
   python manage.py runserver
   ```

9. **Access the Application**
   - Open browser and go to `http://127.0.0.1:8000`
   - Admin panel: `http://127.0.0.1:8000/admin`

## ⚙️ Configuration

### Environment Variables (Production)

Create a `.env` file for production settings:

```env
SECRET_KEY=your-secret-key-here
DEBUG=False
ALLOWED_HOSTS=yourdomain.com,www.yourdomain.com
DATABASE_URL=postgres://user:password@localhost:5432/social_network
```

### Settings Configuration

#### Development Settings (`settings.py`)

```python
DEBUG = True
ALLOWED_HOSTS = []

DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.sqlite3',
        'NAME': BASE_DIR / 'db.sqlite3',
    }
}
```

#### Production Settings

```python
DEBUG = False
ALLOWED_HOSTS = ['yourdomain.com', 'www.yourdomain.com']

DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.postgresql',
        'NAME': 'social_network',
        'USER': 'your_db_user',
        'PASSWORD': 'your_db_password',
        'HOST': 'localhost',
        'PORT': '5432',
    }
}
```

### Media Files Configuration

```python
MEDIA_URL = '/media/'
MEDIA_ROOT = BASE_DIR / 'media'

# For production with cloud storage
DEFAULT_FILE_STORAGE = 'storages.backends.s3boto3.S3Boto3Storage'
AWS_STORAGE_BUCKET_NAME = 'your-bucket-name'
```

## 📖 Usage Guide

### For Regular Users

#### 1. **Account Creation & Setup**

- Visit the welcome page
- Click "Sign Up" and create an account
- Complete your profile with bio, profile picture, birthday, and location
- Start connecting with friends

#### 2. **Creating Content**

- **New Post**: Click "Create Post" from the main feed
- **Visibility Options**:
  - 🌍 **Public**: Visible to everyone
  - 👥 **Friends**: Visible to friends only
  - 🔒 **Private**: Visible only to you
- **Rich Text**: Add formatted content to your posts

#### 3. **Social Interactions**

- **Liking Posts**: Click the heart icon on any post
- **Commenting**: Add comments to engage with posts
- **Friend Requests**: Send, accept, or decline friend requests
- **Profile Visits**: View other users' profiles and posts

#### 4. **Friend Management**

- **Send Friend Requests**: Visit someone's profile and click "Add Friend"
- **Manage Requests**: View pending friend requests in notifications
- **Friend Suggestions**: Discover new people in the "Connect" section
- **Unfriend**: Remove friends from their profile page

#### 5. **Notifications**

- **Real-time Updates**: Get notified about likes, comments, friend requests
- **Notification Center**: View all notifications in one place
- **Mark as Read**: Individual or bulk notification management

### For Moderators

#### 1. **Accessing Moderator Tools**

- Login with moderator account
- Access moderator dashboard from the main navigation
- View comprehensive user and content overview

#### 2. **User Management**

- **Ban/Unban Users**: Temporarily restrict user access
- **View User Activity**: Monitor user behavior and content
- **User Statistics**: Track user engagement and activity

#### 3. **Content Moderation**

- **Delete Posts**: Remove inappropriate content
- **Monitor Reports**: Review flagged content
- **Content Analytics**: Track platform content trends

### For Administrators

#### 1. **Django Admin Interface**

- Access `/admin/` with superuser credentials
- Manage all users, posts, comments, and notifications
- Configure user groups and permissions
- Database administration and backup

#### 2. **System Maintenance**

- **Database Migrations**: Apply schema changes
- **Static File Management**: Update CSS/JS assets
- **Media File Cleanup**: Manage uploaded files
- **Performance Monitoring**: Track system metrics

## 🔗 API Endpoints

### Authentication Endpoints

```
POST   /users/signup/                 # User registration
POST   /users/login/                  # User login
POST   /users/logout/                 # User logout
GET    /users/profile/edit/           # Edit profile page
POST   /users/profile/edit/           # Update profile
```

### Social Network Endpoints

```
GET    /                              # Welcome page
GET    /posts/                        # Main feed (friends' posts)
POST   /posts/                        # Create new post
GET    /post/<id>/                    # View individual post
POST   /post/<id>/like/               # Toggle post like
GET    /post/<id>/likes/              # View post likes
POST   /post/<id>/edit/               # Edit post
DELETE /post/<id>/delete/             # Delete post

GET    /profile/<username>/           # View user profile
GET    /profile/<username>/friends/   # View user's friends
POST   /unfriend/<username>/          # Remove friend

POST   /friend-request/send/<username>/     # Send friend request
POST   /friend-request/cancel/<username>/   # Cancel friend request
POST   /friend-request/accept/<username>/   # Accept friend request
POST   /friend-request/decline/<username>/  # Decline friend request

GET    /notifications/                # View notifications
POST   /notifications/update/         # Mark notifications as read
DELETE /notifications/delete/<id>/    # Delete single notification
DELETE /notifications/delete-all/     # Delete all notifications
GET    /notifications/count/          # Get unread count

GET    /search/                       # User search
GET    /explore/                      # Explore content
GET    /connect/                      # Friend suggestions
```

### Comment Endpoints

```
POST   /post/<id>/comment/            # Add comment to post
GET    /comment/<id>/edit/            # Edit comment
POST   /comment/<id>/edit/            # Update comment
DELETE /comment/<id>/delete/          # Delete comment
```

### Moderation Endpoints

```
GET    /moderator/                    # Moderator dashboard
POST   /moderator/toggle-ban/<id>/    # Ban/unban user
DELETE /moderator/delete-post/<id>/   # Delete any post
```

## 👥 User Roles & Permissions

The application has three user levels with different capabilities:

**Regular Users** can create posts, like and comment on content, send friend requests, and manage their own profiles and content.

**Moderators** have all regular user permissions plus the ability to delete any post and ban/unban users. They also have access to a special moderator dashboard.

**Administrators** have full system access including Django admin interface, user group management, and system configuration.

## 🔒 Security Features

### Authentication Security

- **Password Hashing**: Django's built-in PBKDF2 password hashing
- **Session Management**: Secure session handling with Django sessions
- **CSRF Protection**: Cross-Site Request Forgery protection on all forms
- **Login Protection**: Failed login attempt monitoring

### Data Security

- **SQL Injection Prevention**: Django ORM protection
- **XSS Prevention**: Automatic template escaping
- **File Upload Security**: Image validation with Pillow
- **Permission-Based Access**: Role-based access control

### Privacy Controls

- **Post Visibility**: Three-level privacy settings (Public, Friends, Private)
- **Profile Privacy**: User-controlled profile information sharing
- **Friend-Only Content**: Restricted content access based on friend relationships
- **User Blocking**: Ban functionality for problematic users

### Input Validation

```python
# Form validation examples
class PostForm(forms.ModelForm):
    def clean_content(self):
        content = self.cleaned_data['content']
        if len(content.strip()) < 1:
            raise forms.ValidationError("Post content cannot be empty.")
        return content
```

## 🔧 Development

### Setting Up Development Environment

1. **Enable Debug Mode**

   ```python
   DEBUG = True
   ALLOWED_HOSTS = ['localhost', '127.0.0.1']
   ```

2. **Development Database**

   ```bash
   # Use SQLite for development
   python manage.py migrate
   python manage.py loaddata fixtures/sample_data.json  # If available
   ```

3. **Create Test Data**

   ```python
   # management/commands/create_test_data.py
   from django.core.management.base import BaseCommand
   from users.models import CustomUser
   from network.models import Post, FriendRequest

   class Command(BaseCommand):
       def handle(self, *args, **options):
           # Create test users and sample data
   ```

### Running Tests

```bash
# Run all tests
python manage.py test

# Run specific app tests
python manage.py test users
python manage.py test network

# Run with coverage
pip install coverage
coverage run --source='.' manage.py test
coverage report
coverage html
```

### Code Quality Tools

```bash
# Install development dependencies
pip install flake8 black isort

# Format code
black .
isort .

# Lint code
flake8 .
```

### Database Management

```bash
# Create new migration
python manage.py makemigrations

# Apply migrations
python manage.py migrate

# Reset database (development only)
python manage.py flush

# Database shell
python manage.py dbshell
```

### Debugging

```python
# Add to views for debugging
import pdb; pdb.set_trace()

# Or use Django debug toolbar
pip install django-debug-toolbar
```

## 🚀 Deployment

### Production Setup

1. **Security Configuration**: Set `DEBUG=False`, configure `SECRET_KEY`, and add your domain to `ALLOWED_HOSTS`

2. **Database**: Switch from SQLite to PostgreSQL for production use

3. **Static Files**: Configure static file serving and consider using a CDN

4. **Environment Variables**: Use environment variables for sensitive settings

5. **Web Server**: Deploy with Gunicorn and Nginx for production traffic

### Basic Deployment Steps

```bash
# Set environment variables
export SECRET_KEY="your-secret-key"
export DEBUG=False

# Install production dependencies
pip install gunicorn psycopg2-binary

# Collect static files
python manage.py collectstatic

# Run migrations
python manage.py migrate

# Start with Gunicorn
gunicorn social_network.wsgi:application
```

## 🤝 Contributing

### How to Contribute

1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Add tests for new functionality
5. Ensure all tests pass
6. Submit a pull request

### Guidelines

- Follow PEP 8 Python style guide
- Write unit tests for new features
- Update documentation for significant changes
- Keep commits focused and well-described

### Issue Reporting

When reporting issues, please include:

- Steps to reproduce
- Expected vs actual behavior
- Error messages if any
- Your environment details

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 🙏 Acknowledgments

- Django Framework for the robust foundation
- Django community for excellent documentation
- Contributors and testers
- Open source libraries that made this possible

## 📞 Support

For support, please:

1. Check the documentation
2. Search existing issues
3. Create a new issue with detailed information
4. Contact the development team

## 🔮 Future Enhancements

Some ideas for future development:

- **Real-time Chat**: WebSocket-based messaging between users
- **Group Creation**: User communities and group discussions
- **Enhanced Media**: Photo albums and video post support
- **Mobile App**: React Native companion application
- **Advanced Search**: Full-text search capabilities
- **Analytics**: User engagement and platform metrics
- **Email Notifications**: Configurable email alerts
- **Two-Factor Authentication**: Enhanced account security

---

Built with ❤️ using Django

Last updated: July 2025
