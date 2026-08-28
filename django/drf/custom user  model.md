```python
from django.db import models
from django.contrib.auth.models import AbstractBaseUser, PermissionsMixin
from django.utils.translation import gettext_lazy as _
import uuid

from .managers import UserManager


class User(AbstractBaseUser, PermissionsMixin):

    ROLE_CHOICES = (
        ("student", "Student"),
        ("teacher", "Teacher"),
        ("admin", "Admin"),
    )

    id = models.UUIDField(
        primary_key=True,
        default=uuid.uuid4,
        editable=False
    )

    email = models.EmailField(
        unique=True
    )

    full_name = models.CharField(
        max_length=150
    )

    phone = models.CharField(
        max_length=20,
        blank=True,
        null=True
    )

    profile_image = models.ImageField(
        upload_to="users/profile/",
        blank=True,
        null=True
    )

    role = models.CharField(
        max_length=20,
        choices=ROLE_CHOICES,
        default="student"
    )

    is_active = models.BooleanField(
        default=True
    )

    is_staff = models.BooleanField(
        default=False
    )

    is_verified = models.BooleanField(
        default=False
    )

    created_at = models.DateTimeField(
        auto_now_add=True
    )

    updated_at = models.DateTimeField(
        auto_now=True
    )


    objects = UserManager()


    USERNAME_FIELD = "email"
    REQUIRED_FIELDS = [
        "full_name"
    ]


    def __str__(self):
        return self.email
    
    
    
    
```


```python
from django.contrib.auth.base_user import BaseUserManager


class UserManager(BaseUserManager):

    def create_user(
        self,
        email,
        full_name,
        password=None,
        **extra_fields
    ):

        if not email:
            raise ValueError(
                "Email is required"
            )

        email = self.normalize_email(email)

        user = self.model(
            email=email,
            full_name=full_name,
            **extra_fields
        )

        user.set_password(password)
        user.save()

        return user


    def create_superuser(
        self,
        email,
        full_name,
        password=None,
        **extra_fields
    ):

        extra_fields.setdefault(
            "is_staff",
            True
        )

        extra_fields.setdefault(
            "is_superuser",
            True
        )

        extra_fields.setdefault(
            "role",
            "admin"
        )

        return self.create_user(
            email,
            full_name,
            password,
            **extra_fields
        )
```

