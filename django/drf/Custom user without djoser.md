# model

```python
from django.db import models
from django.contrib.auth.models import AbstractUser
from users.managers import CustomUser
# Create your models here.

class User(AbstractUser):
    username=None #remove username
    email = models.EmailField(unique=True)
    first_name = models.CharField(max_length=100)
    last_name = models.CharField(max_length=100)

    address = models.TextField(blank=True,null=True)
    phone_number = models.CharField(max_length=15,blank=True,null=True)

    USERNAME_FIELD='email'
    REQUIRED_FIELDS=[]

    objects = CustomUser()

    def __str__(self):
        return self.email
```

# manager
```python
from django.contrib.auth.base_user import BaseUserManager

class CustomUser(BaseUserManager):
    def create_user(self,email,password=None, **extra_fields):
        if not email:
            raise ValueError('Email is Required')
        

        email = self.normalize_email(email)
        user = self.model(email=email, **extra_fields)
        user.set_password(password)
        user.save()

        return user
    
    def create_superuser(self, email, password=None, **extra_fields):
        if not email:
            raise ValueError("Email required")

        extra_fields.setdefault('is_staff', True)
        extra_fields.setdefault('is_superuser', True)

        if extra_fields.get('is_staff') is not True:
            raise ValueError('Superuser must have is_staff=True.')

        if extra_fields.get('is_superuser') is not True:
            raise ValueError('Superuser must have is_superuser=True.')

        return self.create_user(email, password, **extra_fields)
```

# setting 
```python
#custom user model add
AUTH_USER_MODEL = 'users.User'
```

# `serializer`
```python
from rest_framework import serializers
from django.contrib.auth import get_user_model,authenticate


User = get_user_model()

class SignUpSerializer(serializers.ModelSerializer):
    password = serializers.CharField(write_only=True)
    class Meta:
        model = User
        fields=['id','email','password','first_name','last_name','address','phone_number']

    def create(self, validated_data):
        password = validated_data.pop('password')
        user = User(**validated_data)
        user.set_password(password)
        user.save()

        return user



class SignInSerializer(serializers.Serializer):
    email = serializers.EmailField()
    password = serializers.CharField(write_only=True)

    def validate(self, data):
        email = data.get('email')
        password = data.get('password')

        if email and password:
            user = authenticate(email=email, password=password)
            if not user:
                raise serializers.ValidationError("Invalid Credentials")
        else:
            raise serializers.ValidationError("Email and password required")

        data['user'] = user
        return data
    
    
```


# views

```python
from django.shortcuts import render
from rest_framework.views import APIView
from rest_framework.response import Response
from rest_framework import status
from users.serializers import SignUpSerializer,SignInSerializer
from rest_framework_simplejwt.tokens import RefreshToken
# Create your views here.

class SignUpAPIView(APIView):
    def post(self,request):
        serializer = SignUpSerializer(data=request.data)
        if serializer.is_valid():
            return Response({'message':'user signup successfully'})
        return Response(serializer.errors,status=status.HTTP_400_BAD_REQUEST)

class SignInAPIView(APIView):
    def post(self,request):
        serializer = SignInSerializer(data=request.data)

        if serializer.is_valid():
            user = serializer.validated_data['user']

            refresh = RefreshToken.for_user(user)

            return Response(
                {
                    'refresh':str(refresh),
                    'access':str(refresh.access_token)
                }
            )
        
        return Response(serializer.errors,status=status.HTTP_400_BAD_REQUEST)



```

# url

```python

from django.contrib import admin
from django.urls import path,include
from users.views import SignUpAPIView, SignInAPIView

urlpatterns = [
    path('admin/', admin.site.urls),
    path("api-auth/", include("rest_framework.urls")),
    # path('api/',include('task1.urls')),
    path('api/signup/', SignUpAPIView.as_view()),
    path('api/signin/', SignInAPIView.as_view())
]

```

create super user, sign-up, sign-in success all operation